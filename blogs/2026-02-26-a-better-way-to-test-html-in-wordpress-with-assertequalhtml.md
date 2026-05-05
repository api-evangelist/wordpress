---
title: "A better way to test HTML in WordPress with assertEqualHTML()"
url: "https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/"
date: "Thu, 26 Feb 2026 16:49:38 +0000"
author: "JuanMa Garrido"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">If you&#8217;ve written PHPUnit tests for WordPress plugins that produce HTML output — block render callbacks, formatting filters, shortcodes — you know the frustration. The test passes on your machine. Then it fails on CI because an attribute comes back in a different order. Or you add a trailing semicolon to an inline style, and suddenly three tests break — even though the browser renders exactly the same thing.</p>



<p class="wp-block-paragraph">WordPress 6.9 introduced a new assertion — <code>assertEqualHTML()</code> — available on <code>WP_UnitTestCase</code> that solves this. It compares HTML semantically, not literally. Attribute order, class name order, style whitespace, attribute quoting style differences — none of those trigger a failure. The test breaks only when the markup is semantically different.</p>



<p class="wp-block-paragraph">This article walks through how to use <code>assertEqualHTML()</code>, what it normalizes, and how to replace fragile string assertions in your existing test suite.</p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#the-problem-with-assertsame-for-html">The problem with assertSame() for HTML</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#what-assertequalhtml-does">What assertEqualHTML() does</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#basic-usage">Basic usage</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#testing-html-api-transformations">Testing HTML API transformations</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#testing-block-render-callbacks">Testing block render callbacks</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#testing-interactivity-api-directive-injection">Testing Interactivity API directive injection</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#understanding-failure-output">Understanding failure output</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#adding-a-custom-failure-message">Adding a custom failure message</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#when-to-keep-assertsame">When to keep assertSame</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#migration-tips">Migration tips</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/#resources">Resources</a></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="the-problem-with-assertsame-for-html">The problem with assertSame() for HTML</h2>



<p class="wp-block-paragraph">Consider a filter that uses the HTML API to add <code>loading="lazy"</code> to images in post content:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">function my_plugin_lazy_load_images( string $content ): string {
    $processor = new WP_HTML_Tag_Processor( $content );
    while ( $processor-&gt;next_tag( 'img' ) ) {
        $processor-&gt;set_attribute( 'loading', 'lazy' );
    }
    return $processor-&gt;get_updated_html();
}
add_filter( 'the_content', 'my_plugin_lazy_load_images' );</code></pre>



<p class="wp-block-paragraph">A test using <code>assertSame()</code> looks like this:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">public function test_lazy_load_images_adds_loading_attribute(): void {
    $input    = '&lt;p&gt;&lt;img src="photo.jpg" alt="A photo" class="size-full"&gt;&lt;/p&gt;';
    $expected = '&lt;p&gt;&lt;img loading="lazy" src="photo.jpg" alt="A photo" class="size-full"&gt;&lt;/p&gt;';

    $this-&gt;assertSame( $expected, my_plugin_lazy_load_images( $input ) );
}</code></pre>



<p class="wp-block-paragraph">This test is fragile. The HTML API inserts <code>loading="lazy"</code> as the first attribute. Your expected string must match that exact position. The moment a future WordPress version changes attribute serialization order — or you switch to a different parser — the test fails, even though the browser renders the same thing.</p>



<p class="wp-block-paragraph">The test is also fragile when the underlying code is legitimately refactored. If you clean up the HTML input to use double quotes consistently, or normalize class name order in your filter, every assertion needs updating.</p>



<div class="wp-block-wporg-notice is-tip-notice"><div class="wp-block-wporg-notice__icon"></div><div class="wp-block-wporg-notice__content"><p>All the examples and tests referenced in this article are available in the following repository: <br /><a href="https://github.com/wptrainingteam/assert-equal-html-examples">https://github.com/wptrainingteam/assert-equal-html-examples</a><br />You can clone the repository and run the tests locally to explore the examples in more detail.</p></div></div>



<h2 class="wp-block-heading" id="what-assertequalhtml-does">What assertEqualHTML() does</h2>



<p class="wp-block-paragraph"><code>assertEqualHTML()</code> is a method on <code>WP_UnitTestCase</code> added in WordPress 6.9 (<a href="https://core.trac.wordpress.org/ticket/63527">#63527</a>, <a href="https://github.com/WordPress/wordpress-develop/pull/8882">PR #8882</a>). It works by parsing both HTML strings into a normalized tree with <code>WP_HTML_Processor</code> and comparing those trees with <code>assertSame</code> &#8211; so two strings that produce the same tree are treated as equal, even if their raw text differs.</p>



<p class="wp-block-paragraph">The normalization handles everything that doesn&#8217;t affect what a browser renders:</p>



<figure class="wp-block-table"><table class="has-fixed-layout"><thead><tr><th class="has-text-align-left">What differs</th><th class="has-text-align-left">assertSame()</th><th class="has-text-align-left">assertEqualHTML()</th></tr></thead><tbody><tr><td class="has-text-align-left">Attribute order</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Class name order</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Style whitespace / trailing <code>;</code></td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Tag name capitalization</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">HTML character references(<code>&amp;not;</code> vs <code>¬</code>)</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Duplicate attributes (HTML spec: first wins)</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Block comment attribute order</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Block class name order</td><td class="has-text-align-left"><img alt="❌" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/274c.png" style="height: 1em;" /> fails</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> passes</td></tr><tr><td class="has-text-align-left">Different HTML content</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td></tr><tr><td class="has-text-align-left">Different attribute values</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td></tr><tr><td class="has-text-align-left">Missing / extra attributes</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td></tr><tr><td class="has-text-align-left">Different class names (not just order)</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td></tr><tr><td class="has-text-align-left">Different style values</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td><td class="has-text-align-left"><img alt="✅" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2705.png" style="height: 1em;" /> catches</td></tr></tbody></table></figure>



<p class="wp-block-paragraph">The method signature is:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">public function assertEqualHTML(
    string  $expected,
    string  $actual,
    ?string $fragment_context = '&lt;body&gt;',
    string  $message = 'HTML markup was not equivalent.'
): void</code></pre>



<h2 class="wp-block-heading" id="basic-usage">Basic usage</h2>



<p class="wp-block-paragraph">Rewriting the earlier test to use <code>assertEqualHTML()</code> makes it resilient to attribute ordering:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">public function test_lazy_load_images_adds_loading_attribute(): void {
    $input    = '&lt;p&gt;&lt;img src="photo.jpg" alt="A photo" class="size-full"&gt;&lt;/p&gt;';
    $expected = '&lt;p&gt;&lt;img src="photo.jpg" alt="A photo" class="size-full" loading="lazy"&gt;&lt;/p&gt;';

    $this-&gt;assertEqualHTML( $expected, my_plugin_lazy_load_images( $input ) );
}</code></pre>



<p class="wp-block-paragraph">Now the exact position of <code>loading="lazy"</code> in the attribute list doesn&#8217;t matter. Both <code>&lt;img loading="lazy" src="..." alt="..."&gt;</code> and <code>&lt;img src="..." alt="..." loading="lazy"&gt;</code> produce the same tree representation, so the assertion passes.</p>



<p class="wp-block-paragraph">The assertion also handles HTML character reference equivalence. Any given character has multiple representations — literal, named, decimal, hex, padded variants, even named references without a semicolon — and <code>assertEqualHTML()</code> treats them all as equal:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">$expected = &lt;&lt;&lt;HTML
&lt;meta
    not-literal="¬"
    not-named="¬"
    not-decimal="¬"
    not-decimal-padded="¬"
    not-hex="¬"
    not-hex-padded="¬"
&gt;
HTML;
$actual = &lt;&lt;&lt;HTML
&lt;meta
    not-literal="¬"
    not-named="&amp;not;"
    not-decimal="&amp;#172;"
    not-decimal-padded="&amp;#0172;"
    not-hex="&amp;#xAC;"
    not-hex-padded="&amp;#x0000AC;"
&gt;
HTML;
$this-&gt;assertEqualHTML( $expected, $actual );</code></pre>



<h2 class="wp-block-heading" id="testing-html-api-transformations">Testing HTML API transformations</h2>



<p class="wp-block-paragraph">Here&#8217;s a more complete example: a plugin function that wraps external links in a <code>&lt;span&gt;</code> for styling, injects a <code>data-external</code> attribute and appends <code>noopener noreferrer</code> to the <code>rel</code> attribute using the HTML API.</p>



<pre class="wp-block-code"><code class="language-php" lang="php">function my_plugin_mark_external_links( string $content ): string {
    $processor = new WP_HTML_Tag_Processor( $content );

    while ( $processor-&gt;next_tag( 'a' ) ) {
        $href = $processor-&gt;get_attribute( 'href' );

        if ( $href &amp;&amp; str_starts_with( $href, 'http' ) &amp;&amp; ! str_contains( $href, home_url() ) ) {
            $processor-&gt;set_attribute( 'data-external', 'true' );
            $rel = $processor-&gt;get_attribute( 'rel' );
            $processor-&gt;set_attribute( 'rel', trim( ( $rel ?? '' ) . ' noopener noreferrer' ) );
        }
    }

    return $processor-&gt;get_updated_html();
}</code></pre>



<p class="wp-block-paragraph">Testing this with <code>assertSame() would</code> require knowing the exact order WordPress serializes <code>data-external</code> and <code>rel</code> relative to existing attributes. With <code>assertEqualHTML</code>, you only need to describe the expected semantic result:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">public function test_external_links_get_marked(): void {
    $input = '&lt;p&gt;Visit &lt;a href="https://example.com" class="external-link"&gt;example.com&lt;/a&gt;&lt;/p&gt;';

    $expected = '&lt;p&gt;Visit &lt;a href="https://example.com" class="external-link" data-external="true" rel="noopener noreferrer"&gt;example.com&lt;/a&gt;&lt;/p&gt;';

    $this-&gt;assertEqualHTML( $expected, my_plugin_mark_external_links( $input ) );
}

public function test_internal_links_are_unchanged(): void {
    $input    = '&lt;p&gt;Read &lt;a href="' . home_url( '/about' ) . '"&gt;about us&lt;/a&gt;&lt;/p&gt;';
    $expected = $input;

    $this-&gt;assertEqualHTML( $expected, my_plugin_mark_external_links( $input ) );
}</code></pre>



<p class="wp-block-paragraph">No matter what order the HTML API serializes the new attributes, both tests correctly verify the semantic intent.</p>



<h2 class="wp-block-heading" id="testing-block-render-callbacks">Testing block render callbacks</h2>



<p class="wp-block-paragraph">Block render callbacks often produce complex markup with deeply nested elements. The <code>assertEqualHTML()</code> assertion is especially useful here because block serialization can produce minor whitespace or attribute-order variations depending on the WordPress version.</p>



<p class="wp-block-paragraph">Consider a dynamic block that renders a card component:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">function my_plugin_render_card_block( array $attributes, string $content ): string {
    $tag = new WP_HTML_Tag_Processor(
        '&lt;div class="wp-block-my-plugin-card"&gt;&lt;/div&gt;'
    );
    $tag-&gt;next_tag();

    if ( ! empty( $attributes['backgroundColor'] ) ) {
        $tag-&gt;set_attribute(
            'style',
            'background-color: ' . esc_attr( $attributes['backgroundColor'] ) . ';'
        );
    }

    if ( ! empty( $attributes['className'] ) ) {
        foreach ( explode( ' ', $attributes['className'] ) as $class ) {
            $tag-&gt;add_class( $class );
        }
    }

    return str_replace(
        '&lt;/div&gt;',
        $content . '&lt;/div&gt;',
        $tag-&gt;get_updated_html()
    );
}</code></pre>



<p class="wp-block-paragraph">The function above creates a wrapper <code>&lt;div&gt;</code> using <code>WP_HTML_Tag_Processor</code>, then conditionally applies a background-color style and appends extra class names based on the block&#8217;s attributes. The content is injected by replacing the closing tag. This gives us a function with several moving parts &#8211; the kind of output <code>assertEqualHTML</code> handles well.</p>



<p class="wp-block-paragraph">Testing the full block output — including the wrapper attributes — looks like this:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">public function test_card_block_renders_with_background_color(): void {
    $attributes = array(
        'backgroundColor' =&gt; '#f5f5f5',
        'className'       =&gt; 'is-style-outlined my-custom-class',
    );

    $inner_content = '&lt;p class="wp-block-paragraph"&gt;Hello&lt;/p&gt;';

    $output = my_plugin_render_card_block( $attributes, $inner_content );

$expected = &lt;&lt;&lt;'HTML'
&lt;div
        class="is-style-outlined my-custom-class wp-block-my-plugin-card"
        style="background-color: #f5f5f5;"
    &gt;&lt;p class="wp-block-paragraph"&gt;Hello&lt;/p&gt;&lt;/div&gt;
    HTML;

    $this-&gt;assertEqualHTML( $expected, $output );
}</code></pre>



<p class="wp-block-paragraph">With <code>assertEqualHTML()</code>, you can write the expected HTML in a readable, well-indented format <a href="https://php.watch/versions/7.3/relaxed-heredoc-nowdoc">using NOWDOC syntax</a> (<code>&lt;&lt;&lt;'HTML'</code>), which avoids variable interpolation and keeps the markup clean. The comparison normalizes attribute order and class names — so <code>is-style-outlined my-custom-class wp-block-my-plugin-card</code> and <code>wp-block-my-plugin-card is-style-outlined my-custom-class</code> are equivalent.</p>



<h2 class="wp-block-heading" id="testing-interactivity-api-directive-injection">Testing Interactivity API directive injection</h2>



<p class="wp-block-paragraph">One of the most common places to reach for <code>assertEqualHTML()</code> is when testing filters that inject <a href="https://developer.wordpress.org/block-editor/reference-guides/interactivity-api/directives-and-store/">Interactivity API directives</a> into block HTML. These filters add <code>data-wp-*</code> attributes to elements — and the exact position of those attributes in the output is irrelevant to the Interactivity API&#8217;s behavior.</p>



<p class="wp-block-paragraph">Here&#8217;s an example: a plugin that hooks into <code>render_block</code> to add Interactivity API context and directives to a list block to toggle expanded state on mouse click.</p>



<pre class="wp-block-code"><code class="language-php" lang="php">function my_plugin_add_list_interactivity( string $block_content, array $block ): string {
    if ( 'core/list' !== $block['blockName'] ) {
        return $block_content;
    }

    $p = new WP_HTML_Tag_Processor( $block_content );

    if ( $p-&gt;next_tag( 'ul' ) ) {
        $p-&gt;set_attribute( 'data-wp-interactive', 'my-plugin/list' );
        $p-&gt;set_attribute( 'data-wp-context', wp_json_encode( array( 'expanded' =&gt; false ) ) );
    }

    while ( $p-&gt;next_tag( 'li' ) ) {
        $p-&gt;set_attribute( 'data-wp-on--click', 'actions.toggle' );
    }

    return $p-&gt;get_updated_html();
}
add_filter( 'render_block', 'my_plugin_add_list_interactivity', 10, 2 );</code></pre>



<p class="wp-block-paragraph">Writing a test for this filter:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">public function test_list_block_gets_interactivity_directives(): void {
    $input = '
        &lt;ul class="wp-block-list"&gt;
            &lt;li&gt;First item&lt;/li&gt;
            &lt;li&gt;Second item&lt;/li&gt;
        &lt;/ul&gt;
    ';

    $block = array( 'blockName' =&gt; 'core/list' );

    $output = my_plugin_add_list_interactivity( $input, $block );

    $expected = '
        &lt;ul
            class="wp-block-list"
            data-wp-interactive="my-plugin/list"
            data-wp-context="{&amp;quot;expanded&amp;quot;:false}"
        &gt;
            &lt;li data-wp-on--click="actions.toggle"&gt;First item&lt;/li&gt;
            &lt;li data-wp-on--click="actions.toggle"&gt;Second item&lt;/li&gt;
        &lt;/ul&gt;
    ';

    $this-&gt;assertEqualHTML( $expected, $output );
}</code></pre>



<p class="wp-block-paragraph">The <code>data-wp-context</code> attribute contains JSON. Whether your function outputs <code>{"expanded":false}</code> or <code>{&amp;quot;expanded&amp;quot;:false}</code>, the HTML API decodes entity references before comparison, so the assertion handles both forms correctly.</p>



<h2 class="wp-block-heading" id="understanding-failure-output">Understanding failure output</h2>



<p class="wp-block-paragraph">When <code>assertEqualHTML()</code> fails, the error message shows the normalized tree representation of both strings — not the raw HTML diff. This makes it much easier to spot meaningful differences.</p>



<p class="wp-block-paragraph">Here&#8217;s an example. Suppose a filter accidentally drops the <code>rel</code> attribute:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">HTML markup was not equivalent.
Failed asserting that two strings are equal.
--- Expected
+++ Actual
@@ @@
 &lt;a&gt;
   href="https://example.com"
+  rel="noopener noreferrer"
   "example.com"</code></pre>



<p class="wp-block-paragraph">Compare this to a <code>assertSame()</code> failure for the same problem:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">Failed asserting that two strings are equal.
--- Expected
+++ Actual
@@ @@
-&lt;a href="https://example.com" rel="noopener noreferrer"&gt;example.com&lt;/a&gt;
+&lt;a href="https://example.com"&gt;example.com&lt;/a&gt;</code></pre>



<p class="wp-block-paragraph">Both show the missing <code>rel</code>, but the tree format from <code>assertEqualHTML()</code> also works well for complex, deeply nested block markup — each attribute on its own line, consistently indented. When a test fails on a render callback that outputs 20+ lines of HTML, the tree diff pinpoints exactly which attribute on which element changed.</p>



<p class="wp-block-paragraph">The tree format also understands block delimiters. For block markup, it renders blocks as <code>BLOCK["namespace/name"]</code> with their attributes as formatted JSON, separate from the HTML structure. That means a test for block output shows both the block attribute changes and the HTML attribute changes in separate, readable sections.</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">Failed asserting that two strings are identical.
---·Expected
+++·Actual
@@ @@
  class="wp-block-group"
  BLOCK["core/paragraph"]
    {
-········"align":·"center"
+········"align":·"left"
    }
    " 
  "
&lt;p&gt;
-········class="has-text-align-center"
+········class="has-text-align-left"
"Hello world"
    "
  "</code></pre>



<h2 class="wp-block-heading" id="adding-a-custom-failure-message">Adding a custom failure message</h2>



<p class="wp-block-paragraph">Pass a custom message as the fourth argument to make failures easier to identify:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">$this-&gt;assertEqualHTML( $expected, $actual, '&lt;body&gt;', 'Card block output did not match.' );</code></pre>



<p class="wp-block-paragraph">The third argument, <code>$fragment_context</code>, defaults to <code>'&lt;body&gt;'</code> — correct for most WordPress content and block output. Pass <code>null</code> to compare full HTML documents. When you only need to set a custom message, pass <code>'&lt;body&gt;'</code> explicitly to keep the default parsing context.</p>



<h2 class="wp-block-heading" id="when-to-keep-assertsame">When to keep assertSame</h2>



<p class="wp-block-paragraph"><code>assertEqualHTML()</code> is not a universal replacement for <code>assertSame()</code>. Keep using <code>assertSame()</code> when:</p>



<ul class="wp-block-list">
<li><strong>Exact string output matters</strong> — for example, testing a function that other code feeds back into a parser that requires a specific serialization format.</li>



<li><strong>Testing non-HTML output</strong> — <code>assertEqualHTML()</code> only makes sense for HTML strings.</li>



<li><strong>Testing plain-text output</strong> — for a function that returns a string with no HTML markup at all (e.g., the output of <code>strip_tags()</code>), use <code>assertSame()</code>. If the output can contain HTML character references, <code>assertEqualHTML()</code> is still the better choice since it normalizes them.</li>
</ul>



<p class="wp-block-paragraph">One specific case where <code>assertSame()</code> is still correct: verifying the exact serialization of a <code>data-wp-context</code> attribute value or the content of a <code>&lt;script&gt;</code> tag. If exact string output matters there, test it directly with <code>assertSame()</code>.</p>



<h2 class="wp-block-heading" id="migration-tips">Migration tips</h2>



<p class="wp-block-paragraph">For existing test suites, the a basic migration path would be to find tests that compare HTML strings with <code>assertSame()</code> and ask, &#8220;Would this test still be meaningful if attribute order changed?&#8221;</p>



<p class="wp-block-paragraph">If yes, switch to <code>assertEqualHTML()</code>. The method is a drop-in replacement for the common pattern:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">// Before:
$this-&gt;assertSame( $expected_html, $actual_html );

// After:
$this-&gt;assertEqualHTML( $expected_html, $actual_html );</code></pre>



<p class="wp-block-paragraph">If your test class extends <code>WP_UnitTestCase</code> (either directly or through a subclass), the method is available immediately in WordPress 6.9+.</p>



<p class="wp-block-paragraph">Some test suites have custom <code>assertEqualMarkup()</code> methods or helpers that parse HTML with <code>DOMDocument</code> before comparing. Those can be replaced with <code>assertEqualHTML()</code> — which uses the more modern <code>WP_HTML_Processor</code> and adds block-awareness on top.</p>



<h2 class="wp-block-heading" id="resources">Resources</h2>



<ul class="wp-block-list">
<li><a href="https://core.trac.wordpress.org/ticket/63527">Tests: Add test assertion to compare HTML for equivalence #63527</a> — TRAC ticket with the original proposal and discussion</li>



<li><a href="https://github.com/WordPress/wordpress-develop/pull/8882">Tests: Add new assertEqualHTML assertion #8882</a> — PR with the implementation</li>



<li><a href="https://make.wordpress.org/core/2025/11/21/updates-to-the-html-api-in-6-9/">Updates to the HTML API in 6.9</a> — dev note by <a class="mention" href="https://profiles.wordpress.org/dmsnell/"><span class="mentions-prefix">@</span>dmsnell</a> covering all HTML API changes in WordPress 6.9</li>



<li><a href="https://developer.wordpress.org/reference/classes/wp_html_tag_processor/">WP_HTML_Tag_Processor reference</a> — for writing the filters you&#8217;ll want to test</li>



<li><a href="https://developer.wordpress.org/block-editor/reference-guides/interactivity-api/">Interactivity API reference</a> — directives and store API</li>



<li><a href="https://github.com/search?q=repo%3AWordPress%2Fwordpress-develop%20assertEqualHTML&amp;type=code">Real-world uses in WordPress core</a> — see how core uses <code>assertEqualHTML()</code> across its test suite</li>
</ul>



<p class="wp-block-paragraph">If you&#8217;ve replaced string-based HTML assertions in your plugin or theme&#8217;s test suite with <code>assertEqualHTML()</code>, share how it worked in the comments — especially if you ran into edge cases worth knowing about.</p>



<p class="wp-block-paragraph"><em>Props to <a class="mention" href="https://profiles.wordpress.org/bph/"><span class="mentions-prefix">@</span>bph</a> and <a class="mention" href="https://profiles.wordpress.org/jonsurrell/"><span class="mentions-prefix">@</span>jonsurrell</a> for reviewing this post</em></p>



<p class="wp-block-paragraph"></p>

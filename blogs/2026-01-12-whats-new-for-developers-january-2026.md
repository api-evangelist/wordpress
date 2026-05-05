---
title: "What’s new for developers? (January 2026)"
url: "https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/"
date: "Mon, 12 Jan 2026 14:22:10 +0000"
author: "Justin Tadlock"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">It’s a brand new year, and that means that another exciting 12 months of WordPress development lies ahead. As usual, I’m optimistic about the future of our beloved platform.</p>



<p class="wp-block-paragraph">The landscape is always changing on the web, and I’m sure the next iteration will come with its challenges and opportunities for growth in our field. Contributors at the Developer Blog are already busily working on new content. I expect that there’ll be much to share and learn in the days, weeks, and months ahead.</p>



<p class="wp-block-paragraph">If you have an interest in contributing more deeply to the next WordPress release, the <a href="https://make.wordpress.org/core/2026/01/09/wordpress-7-0-call-for-volunteers/">version 7.0 call for volunteers</a> was just announced. Also, If you missed it, be sure to check out the <a href="https://make.wordpress.org/core/2025/12/19/wordpress-6-9-release-retrospective/">WordPress 6.9 Release Retrospective</a>. Take the time to fill out the form to share your thoughts before January 15.</p>



<p class="wp-block-paragraph">For now, let’s focus on the past month, which slowed down just a little with the holidays in the mix. In that time, there was only a single Gutenberg release (<a href="https://make.wordpress.org/core/2025/12/17/gutenberg-22-3-december-17/">version 22.3</a>).&nbsp;</p>



<p class="wp-block-paragraph">As usual, when testing features mentioned in these <em>What’s new?</em> posts, ensure that you’re running WordPress trunk and the latest version of the Gutenberg plugin (<a href="https://playground.wordpress.net/?wp=nightly&amp;plugin=gutenberg">test the latest via Playground</a>).</p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#highlights">Highlights</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#responsive-grid-block-with-set-columns">Responsive Grid block with set columns</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#dedicated-font-library-admin-screen">Dedicated Font Library admin screen</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#build-blocks-with-php">Build blocks with PHP</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#plugins-and-tools">Plugins and tools</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#new-image-cropper-package">New Image Cropper package</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#updated-abilities-package">Updated Abilities package</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#data-views-updates">Data Views updates</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#routing-enhancements">Routing enhancements</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#themes">Themes</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#breadcrumbs-block-pushes-forward">Breadcrumbs block pushes forward</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#other-block-library-updates">Other block library updates</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#border-style-flipping-and-rtl">Border-style flipping and RTL</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#navigation-overlay-experiment">Navigation overlay experiment</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#deprecated-pullquote-block-maybe">Deprecated Pullquote block? Maybe</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#playground">Playground</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#resources">Resources</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/whats-new-for-developers-january-2026/#developer-blog">Developer Blog</a></li></ol></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="highlights">Highlights</h2>



<h3 class="wp-block-heading" id="responsive-grid-block-with-set-columns">Responsive Grid block with set columns</h3>



<figure class="wp-block-image alignwide size-full has-custom-border wp-lightbox-container"><img alt="WordPress page editor with a Grid block shown in the content canvas. It has two grid columns. The first shows a quote and two gradient images. The second shows a single image." class="has-border-color has-light-grey-1-border-color wp-image-5743" height="1064" src="https://developer.wordpress.org/news/files/2026/01/grid-responsive.webp" style="border-width: 1px;" width="2048" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">You can now use both the <strong>Minimum column width</strong> and <strong>Columns</strong> controls simultaneously when using the Grid block variation. <a href="https://github.com/WordPress/gutenberg/pull/73662">The latest PR</a>, which is a part of a larger effort to <a href="https://github.com/WordPress/gutenberg/issues/57478">improve grid layout</a>, also removes the toggle between <strong>Auto</strong> and <strong>Manual</strong> modes.</p>



<p class="wp-block-paragraph">Previously, you had to choose between one option or another: minimum column width allowed responsive columns, but setting a specific column count stayed fixed. With this PR, you can combine the two options to have fully responsive columns while defining the number of columns to show.</p>



<h3 class="wp-block-heading" id="dedicated-font-library-admin-screen">Dedicated Font Library admin screen</h3>



<figure class="wp-block-image alignwide size-full wp-lightbox-container"><img alt="WordPress admin showing a screen titled &quot;Fonts.&quot; It displays tabs for the library and uploading. The current library tab displays a list of the theme&apos;s and the user&apos;s custom fonts." class="wp-image-5744" height="1117" src="https://developer.wordpress.org/news/files/2026/01/font-library-screen.webp" width="2048" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">Since its release, font management has been hidden deep within the <strong>Styles</strong> UI in the WordPress admin. This has made it harder to navigate than necessary. This has now changed in Gutenberg 22.3. <a href="https://github.com/WordPress/gutenberg/pull/73630">The latest iteration adds</a> a dedicated <strong>Appearance <span class="wp-exclude-emoji">→</span> Fonts</strong> screen in the admin.</p>



<p class="wp-block-paragraph">The new screen is still being worked on and isn’t in a final state yet. Currently, you can manage installed fonts and upload new ones. However, the <strong>Collections</strong> tab is missing.</p>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/73876">Support for classic themes</a> is already merged in Gutenberg trunk and should ship with Gutenberg 22.4.</p>



<h3 class="wp-block-heading" id="build-blocks-with-php">Build blocks with PHP</h3>



<p class="wp-block-paragraph">Gutenberg 21.8 introduced the ability to register blocks using PHP only (no JavaScript required). Since then, the feature has been updated. PHP-only registration now fully <a href="https://github.com/WordPress/gutenberg/pull/73556">supports all block metadata</a>. The feature is still currently experimental, but you can test it with this PHP code snippet:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">add_action('init', 'pluginslug_register_block_types');

function pluginslug_register_block_types(): void
{
	register_block_type('pluginslug/test', [
		'title'           =&gt; __('My Test Block', 'pluginslug'),
		'icon'            =&gt; 'admin-generic',
		'category'        =&gt; 'widgets',
		'description'     =&gt; __('My test block description.', 'pluginslug'),
		'keywords'        =&gt; [ 'test' ],
		'supports'        =&gt; [ 'auto_register' =&gt; true ],
		'render_callback' =&gt; fn() =&gt; '&lt;p&gt;Hello, world!&lt;/p&gt;'
	]);
}</code></pre>



<h2 class="wp-block-heading" id="plugins-and-tools">Plugins and tools</h2>



<h3 class="wp-block-heading" id="new-image-cropper-package">New Image Cropper package</h3>



<p class="wp-block-paragraph">The new <code>@wordpress/image-cropper</code> package introduces a standardized image-cropping component. Some features include an interactive aspect ratio-based crop area, rotating images, zoom and flip controls, and more.</p>



<p class="wp-block-paragraph">The feature was initially added with <a href="https://github.com/WordPress/gutenberg/pull/72414">basic Storybook examples</a>, but it’s now implemented <a href="https://github.com/WordPress/gutenberg/pull/73277">directly in the editor</a>, improving how media editing and previews work. Developers maintaining image-based blocks can begin exploring this package to align with the new core cropping flow.</p>



<p class="wp-block-paragraph">This is a sub-task from a larger ticket to improvements to the <a href="https://github.com/WordPress/gutenberg/issues/73771">WordPress Media Editor in 7.0</a>.</p>



<h3 class="wp-block-heading" id="updated-abilities-package">Updated Abilities package</h3>



<p class="wp-block-paragraph">Gutenberg 22.2 added the <code>@wordpress/abilities</code> package, <a href="https://github.com/WordPress/gutenberg/pull/72703">which is a client library</a> that provides a standardized way to discover and execute WordPress capabilities.</p>



<p class="wp-block-paragraph">Version 22.3 <a href="https://github.com/WordPress/gutenberg/pull/73428">updated the package</a> so that it can operate as a standalone capabilities layer beyond traditional WordPress contexts. It also adds a separate <code>@wordpress/core-abilities</code> package for WordPress server integration. These updates should pave the way for an Abilities API JavaScript client to be included in WordPress 7.0.</p>



<h3 class="wp-block-heading" id="data-views-updates">Data Views updates</h3>



<p class="wp-block-paragraph">Data Views and Data Forms systems gained several updates aimed at consistency and validation improvements. The updates:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/73465">Add min/max validation</a> for input fields.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73644">Introduce display formats</a> for number and integer types.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73334">Standardize padding</a> across components.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73671">Update operator labels</a> and deprecate <code>isNotAll</code>.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/7307">Add media-specific fields</a> for attachments.</li>
</ul>



<h3 class="wp-block-heading" id="routing-enhancements">Routing enhancements</h3>



<p class="wp-block-paragraph">Recent routing pull requests move Gutenberg further toward an app-like navigation framework. These updates continue to pave the way for fluid SPA-like behavior across the block and site editors.</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/73703">Conditional inspector rendering</a> via <code>route.inspector()</code>.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73620">Mobile-specific rendering</a> support.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73847">Native page title management</a> for routes.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73586">Smooth view transitions</a> between navigations.</li>
</ul>



<h2 class="wp-block-heading" id="themes">Themes</h2>



<h3 class="wp-block-heading" id="breadcrumbs-block-pushes-forward">Breadcrumbs block pushes forward</h3>



<p class="wp-block-paragraph">One of the oft-requested blocks looks to be well on its way to shipping with WordPress 7.0. While we’re still months away from release, the block is in a well-rounded state at this point and covers a lot of use cases. Now is a perfect time to begin testing it with your themes.</p>



<p class="wp-block-paragraph">The latest updates include:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/73794">Support for block alignment</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73670">Support for paged comments</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/73487">Improved homepage handling</a></li>
</ul>



<h3 class="wp-block-heading" id="other-block-library-updates">Other block library updates</h3>



<p class="wp-block-paragraph">Some other updates to the block library shipped with Gutenberg 22.3 are:</p>



<ul class="wp-block-list">
<li><strong>Button:</strong> Migrated to use <a href="https://github.com/WordPress/gutenberg/pull/73732">text-align block support</a>.</li>



<li><strong>Comments Pagination Numbers:</strong> Added margin and padding <a href="https://github.com/WordPress/gutenberg/pull/67267">spacing controls</a>.</li>



<li><strong>Accordion Heading:</strong> Adds <a href="https://github.com/WordPress/gutenberg/pull/73608">default styles for classic themes</a>, correcting a <a href="https://github.com/WordPress/gutenberg/issues/73454">CSS specificity issue</a> in WordPress 6.9 (this should be backported to a minor release).</li>
</ul>



<h3 class="wp-block-heading" id="border-style-flipping-and-rtl">Border-style flipping and RTL</h3>



<p class="wp-block-paragraph">A bug with the block library’s <code>common.css</code> file incorrectly flipped explicitly assigned border styles. A new patch ensures that these <a href="https://github.com/WordPress/gutenberg/pull/44170">borders are not flipped</a> for RTL-generated stylesheets.</p>



<h3 class="wp-block-heading" id="navigation-overlay-experiment">Navigation overlay experiment</h3>



<p class="wp-block-paragraph">The ability to <a href="https://github.com/WordPress/gutenberg/issues/73080">assign a template part</a> for the Navigation block’s overlay could land in a future version of WordPress. One of the earliest experiments around this idea came from right here on the Developer Blog: <a href="https://developer.wordpress.org/news/2024/02/an-introduction-to-block-based-mega-menus/">An introduction to block-based mega menus</a>. And the idea has since made its way into wider community projects. Now the feature is being explored as part of WordPress itself.</p>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/73760">The first version</a> of this feature landed in Gutenberg 22.3, but it is currently <a href="https://github.com/WordPress/gutenberg/pull/73359">flagged as experimental</a>. You can enable it via the <strong>Gutenberg <span class="wp-exclude-emoji">→</span> Experiments</strong> screen in your WordPress admin.</p>



<h3 class="wp-block-heading" id="deprecated-pullquote-block-maybe">Deprecated Pullquote block? Maybe</h3>



<p class="wp-block-paragraph">The <a href="https://github.com/WordPress/gutenberg/pull/73228">Pullquote block was deprecated</a> in Gutenberg 22.2 in favor of using the Quote block. However, the conversation has since picked up after contributors expressed multiple concerns around accessibility, HTML semantics, and block style variations. <a href="https://github.com/WordPress/gutenberg/issues/11610">The original ticket</a> is still open with the ongoing discussion.</p>



<h2 class="wp-block-heading" id="playground">Playground</h2>



<p class="wp-block-paragraph">On Playground, there are <a href="https://make.wordpress.org/playground/2025/12/29/three-new-ui-updates-to-wordpress-playground-from-december-2025/">three new UI updates</a>:</p>



<ul class="wp-block-list">
<li>A dedicated management dashboard</li>



<li>An “Unsaved Playground” warning with Save button</li>



<li>A Quick Access dropdown for common admin pages​</li>
</ul>



<p class="wp-block-paragraph">A new <a href="https://github.com/WordPress/wordpress-playground/pull/3056">DevTools browser extension</a> adds a DevTools panel where you can inspect and edit Playground instances directly inside Chrome. This makes it feel much more like developing in a local environment.</p>



<p class="wp-block-paragraph">Playground can now <a href="https://github.com/WordPress/wordpress-playground/pull/3065">skip the WordPress installation step</a> when WordPress files already exist, which speeds up reusing existing environments and blueprints.​</p>



<p class="wp-block-paragraph">There is also a <a href="https://github.com/WordPress/wordpress-playground/pull/3071">standalone Playground block demo page</a>, providing an interactive code editor with live WordPress Playground preview. It supports multi-file editing, JSX transpilation, file tabs, and more.</p>



<h2 class="wp-block-heading" id="resources">Resources</h2>



<h3 class="wp-block-heading" id="developer-blog">Developer Blog</h3>



<p class="wp-block-paragraph">Two new posts were published on the Developer Blog in the past month, teaching more advanced techniques like automated testing and combining multiple APIs. Give them a read if you haven’t already:</p>



<ul class="wp-block-list">
<li><a href="https://developer.wordpress.org/news/2025/12/how-to-add-automated-unit-tests-to-your-wordpress-plugin/">How to add automated unit tests to your WordPress plugin</a></li>



<li><a href="https://developer.wordpress.org/news/2025/12/word-switcher-extending-core-blocks-with-interactivity/">Word Switcher: Extending Core Blocks with Interactivity</a></li>
</ul>



<p class="has-text-align-right wp-block-paragraph"><em>Props to <a class="mention" href="https://profiles.wordpress.org/psykro/"><span class="mentions-prefix">@</span>psykro</a> and <a class="mention" href="https://profiles.wordpress.org/juanmaguitar/"><span class="mentions-prefix">@</span>juanmaguitar</a> for feedback and review on this article and <a class="mention" href="https://profiles.wordpress.org/bph/"><span class="mentions-prefix">@</span>bph</a> and <a class="mention" href="https://profiles.wordpress.org/fellyph/"><span class="mentions-prefix">@</span>fellyph</a> for contributing notes.</em></p>

---
title: "How to add custom entries to the editor Preview dropdown"
url: "https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/"
date: "Thu, 19 Feb 2026 14:30:31 +0000"
author: "Birgit Pauli-Haack"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="has-manrope-font-family wp-block-paragraph"><a href="https://make.wordpress.org/core/2024/10/18/extending-the-preview-dropdown-menu-in-wordpress-6-7/">Since WordPress 6.7</a>, plugin developers can extend the Preview dropdown in the editor with custom menu items. This is possible through the <code><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-editor/#pluginpreviewmenuitem">PluginPreviewMenuItem</a></code> component from the <code>@wordpress/editor</code> package. This article walks through building a small plugin that adds a “Social Card Preview” option — showing how a post will look when shared on X.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Screenshot of a Preview Menu " class="wp-image-5863" height="373" src="https://developer.wordpress.org/news/files/2026/02/Screenshot-2026-02-18-at-16.20.58.png" width="922" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#what-is-pluginpreviewmenuitem">What is PluginPreviewMenuItem?</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#social-card-preview-example">Social Card Preview example</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#plugin-setup">Plugin setup</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#the-php-bootstrap">The PHP bootstrap</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#build-tooling">Build tooling</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#registering-the-preview-menu-item">Registering the preview menu item</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#building-the-social-card-modal">Building the social card modal</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#the-card-preview-markup">The Card Preview markup</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#styling-the-card">Styling the card</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#testing-with-wordpress-playground">Testing with WordPress Playground</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/#going-further">Going further</a></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="what-is-pluginpreviewmenuitem">What is PluginPreviewMenuItem?</h2>



<p class="wp-block-paragraph">The <strong>Preview</strong> dropdown sits in the editor&#8217;s top bar and lets users preview their content in different ways. Before WordPress 6.7, only Core add items there. With <code>PluginPreviewMenuItem</code> component, plugins can register their own entries in that dropdown. It uses the same <a href="https://developer.wordpress.org/block-editor/reference-guides/components/slot-fill/">Slot/Fill pattern</a> that powers other extension points like <code>PluginMoreMenuItem</code> or <code>PluginSidebar</code>.</p>



<p class="wp-block-paragraph">The component accepts an <code>onClick</code> handler for button behavior or an <code>href</code> for link behavior. You can also pass an optional <code>icon</code> prop. The text you place between the opening and closing <code>&lt;PluginPreviewMenuItem&gt;</code> tags becomes the label shown in the menu.</p>



<h2 class="wp-block-heading" id="social-card-preview-example">Social Card Preview example</h2>



<p class="wp-block-paragraph">This plugin adds a <strong>Social Card Preview</strong> item to the <strong>Preview</strong> dropdown. When clicked, it opens a modal that shows a mock preview of how the current post would appear as an X card. The modal reads the post title, excerpt, and featured image directly from the editor store, so it always reflects the latest unsaved edits. You can take a peek at the <a href="https://github.com/bph/dev-blog-custom-preview">example plugin on GitHub. </a></p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Screenshot of Preview displayed in a modal" class="wp-image-5864" height="708" src="https://developer.wordpress.org/news/files/2026/02/Screenshot-2026-02-18-at-13.47.22.png" width="973" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h2 class="wp-block-heading" id="plugin-setup">Plugin setup</h2>



<p class="wp-block-paragraph">Following along, you start with the file structure. The plugin needs a main PHP file for WordPress to recognize it, a <code>package.json</code> for the build tooling, and the source files in a <code>src/</code> folder.</p>



<pre class="wp-block-code"><code class="language-markdown" lang="markdown">custom-preview/
├── custom-preview.php
├── package.json
└── src/
    ├── index.js
    ├── social-card-preview.js
    └── style.css</code></pre>



<h3 class="wp-block-heading" id="the-php-bootstrap">The PHP bootstrap</h3>



<p class="wp-block-paragraph">The main plugin file, <code>custom-preview.php</code>, registers the script and stylesheet on the <code>enqueue_block_editor_assets</code> hook. The code uses the asset file that <code>@wordpress/scripts</code> generates during the build — it contains the dependency list and a version hash so WordPress can handle caching properly. The below code goes after the <a href="https://developer.wordpress.org/plugins/plugin-basics/header-requirements/">PHP plugin header</a>.</p>



<pre class="wp-block-code has-small-font-size"><code class="language-php" lang="php">function social_card_preview_enqueue_editor_assets() {
	$asset_file = plugin_dir_path( __FILE__ ) . 'build/index.asset.php';

	if ( ! file_exists( $asset_file ) ) {
		return;
	}

	$asset = include $asset_file;

	wp_enqueue_script(
		'social-card-preview-editor',
		plugin_dir_url( __FILE__ ) . 'build/index.js',
		$asset['dependencies'],
		$asset['version'],
		true
	);

	wp_enqueue_style(
		'social-card-preview-editor',
		plugin_dir_url( __FILE__ ) . 'build/style-index.css',
		array(),
		$asset['version']
	);
}
add_action( 'enqueue_block_editor_assets', 'social_card_preview_enqueue_editor_assets' );</code></pre>



<p class="wp-block-paragraph">This is a common pattern in WordPress block editor plugin development. The <code>enqueue_block_editor_assets</code> hook makes sure <a href="https://developer.wordpress.org/block-editor/how-to-guides/enqueueing-assets-in-the-editor/#editor-scripts-and-styles">the script and styles only load inside the editor</a>, not on the frontend. </p>



<h3 class="wp-block-heading" id="build-tooling">Build tooling</h3>



<p class="wp-block-paragraph">For the JavaScript build, <code>@wordpress/scripts</code> handles the tooling. The <code>package.json</code> is minimal:</p>



<pre class="wp-block-code has-small-font-size"><code class="language-json" lang="json">{
	"name": "social-card-preview",
	"version": "1.0.0",
	"scripts": {
		"build": "wp-scripts build",
		"start": "wp-scripts start"
	},
	"devDependencies": {
		"@wordpress/scripts": "^30.0.0"
	}
}</code></pre>



<p class="wp-block-paragraph">Run <code>npm install</code> to get the dependencies, then <code>npm run build</code> to compile. During development, <code>npm run start</code> watches for changes and rebuilds automatically.</p>



<h2 class="wp-block-heading" id="registering-the-preview-menu-item">Registering the preview menu item</h2>



<p class="wp-block-paragraph">The entry point <code>src/index.js</code> is where the plugin is registered and the menu item is added to the Preview dropdown. The idea behind it: render a <code>PluginPreviewMenuItem</code> that, when clicked, opens a modal.</p>



<pre class="wp-block-code has-small-font-size"><code class="language-jsx line-numbers" lang="jsx">import { __ } from '@wordpress/i18n';
import { registerPlugin } from '@wordpress/plugins';
import { PluginPreviewMenuItem } from '@wordpress/editor';
import { useState } from '@wordpress/element';

import SocialCardPreview from './social-card-preview';
import './style.css';

const SocialCardPreviewMenuItem = () =&gt; {
	const [ isOpen, setIsOpen ] = useState( false );

	return (
		&lt;&gt;
			&lt;PluginPreviewMenuItem
				onClick={ () =&gt; setIsOpen( true ) }
			&gt;
				{ __( 'Social Card Preview', 'social-card-preview' ) }
			&lt;/PluginPreviewMenuItem&gt;
			{ isOpen &amp;&amp; (
				&lt;SocialCardPreview
					onClose={ () =&gt; setIsOpen( false ) }
				/&gt;
			) }
		&lt;/&gt;
	);
};

registerPlugin( 'social-card-preview', {
	render: SocialCardPreviewMenuItem,
} );</code></pre>



<p class="wp-block-paragraph">A few things to note here: </p>



<ul class="wp-block-list">
<li>The code uses <code>registerPlugin</code> from <code><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-plugins/">@wordpress/plugins</a></code> to register the component. </li>



<li>The <code>PluginPreviewMenuItem</code> works like any other menu item — give it an <code>onClick</code> and some children for the label. </li>



<li>Modal visibility is managed with a basic <code>useState</code> toggle.</li>
</ul>



<h2 class="wp-block-heading" id="building-the-social-card-modal">Building the social card modal</h2>



<p class="wp-block-paragraph">The <code>SocialCardPreview</code> component reads data from the editor store and renders a mock X card inside a <code>Modal</code>.</p>



<pre class="wp-block-code has-small-font-size"><code class="language-javascript line-numbers" lang="javascript">import { __ } from '@wordpress/i18n';
import { Modal } from '@wordpress/components';
import { useSelect } from '@wordpress/data';
import { store as editorStore } from '@wordpress/editor';
import { store as coreStore } from '@wordpress/core-data';

const SocialCardPreview = ( { onClose } ) =&gt; {
	const { title, excerpt, imageUrl, siteUrl } = useSelect( ( select ) =&gt; {
		const { getEditedPostAttribute } = select( editorStore );
		const featuredMediaId = getEditedPostAttribute( 'featured_media' );

		let featuredImageUrl = '';
		if ( featuredMediaId ) {
			const media = select( coreStore ).getMedia( featuredMediaId );
			featuredImageUrl =
				media?.media_details?.sizes?.large?.source_url ||
				media?.source_url ||
				'';
		}

		return {
			title: getEditedPostAttribute( 'title' ) || '',
			excerpt: getEditedPostAttribute( 'excerpt' ) || '',
			imageUrl: featuredImageUrl,
			siteUrl: select( coreStore ).getSite()?.url || '',
					};
	}, [] );

	const domain = siteUrl ? new URL( siteUrl ).hostname : '';
	const truncatedExcerpt =
		excerpt.length &gt; 200
			? excerpt.substring( 0, 200 ) + '…'
			: excerpt;

	return (
		&lt;Modal title={ __( 'X Preview', 'social-card-preview' ) } 
                       onRequestClose={ onClose } 
                       size="medium"&gt;
			{ /* Card preview markup see below */ }
		&lt;/Modal&gt;
	);
};</code></pre>



<p class="wp-block-paragraph">Here is a breakdown. The <code>useSelect</code> hook pulls the required data from two stores. From the <code>editor</code> store, it retrieves the post title, excerpt, and featured media ID. From the <code>core-data</code> store, it resolves the media ID to an actual image URL and fetches the site URL to display the domain name on the card.</p>



<p class="wp-block-paragraph">For the featured image, the code tries the <code>large</code> size first, falling back to the full <code>source_url</code>. The excerpt gets truncated to 200 characters because that is roughly what X shows.</p>



<p class="wp-block-paragraph">Because <code>useSelect</code> is reactive, the preview updates in real time as you edit the post. Change the title, and the card updates immediately — no need to save first.</p>



<h2 class="wp-block-heading" id="the-card-preview-markup">The Card Preview markup</h2>



<p class="wp-block-paragraph">The card markup mirrors how X renders link previews. The featured image sits at the top, followed by a content area with the domain, title, and truncated excerpt. The image only renders when a featured image exists, thanks to the conditional <code>imageUrl &amp;&amp;</code> check.&nbsp; </p>



<p class="wp-block-paragraph">Each piece of text uses a <code>&lt;span&gt;</code> rather than a heading or paragraph because&nbsp;this is a visual mock — not semantic document content. The class names like <code>social-card-preview__title</code> follow the <a href="https://getbem.com/">BEM (Block Element Modifier)</a> naming&nbsp;convention — <code>social-card-preview</code> is the block, and <code>__title</code>, <code>__domain</code>,&nbsp; <code>__description</code> are elements within it. This keeps the styles scoped and avoids collisions with editor styles.</p>



<p class="wp-block-paragraph">The below text goes between the <code>&lt;Modal&gt;&lt;/Modal&gt;</code> tags in above code example. The complete <code><a href="https://github.com/bph/dev-blog-custom-preview/blob/main/src/social-card-preview.js">social-card-preview.js</a></code> is also on GitHub:</p>



<pre class="wp-block-code has-small-font-size"><code class="language-jsx line-numbers" lang="jsx">&lt;div className="social-card-preview"&gt;
    &lt;div className="social-card-preview__card social-card-preview__card--twitter"&gt;
	{ imageUrl &amp;&amp; (
		&lt;img className="social-card-preview__image"
			src={ imageUrl }
			alt=""
		/&gt;
	) }
      &lt;div className="social-card-preview__content"&gt;
	  &lt;span className="social-card-preview__domain"&gt;
		{ domain }
	  &lt;/span&gt;
          &lt;span className="social-card-preview__title"&gt;
	       { title }
         &lt;/span&gt;
         &lt;span className="social-card-preview__description"&gt;
	         { truncatedExcerpt }
         &lt;/span&gt;
     &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;</code></pre>



<h2 class="wp-block-heading" id="styling-the-card">Styling the card</h2>



<p class="wp-block-paragraph">The CSS approximates how X renders link cards and follows the naming decision from above. </p>



<pre class="wp-block-code"><code class="language-css" lang="css">.social-card-preview__card {
	border: 1px solid #dadce0;
	border-radius: 16px;
	overflow: hidden;
}

.social-card-preview__title {
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
	overflow: hidden;
}</code></pre>



<p class="wp-block-paragraph">The card uses a 16px border radius to match X’s rounded style. The <code>-webkit-line-clamp</code> rules handle text truncation for the title and description.</p>



<h2 class="wp-block-heading" id="testing-with-wordpress-playground">Testing with WordPress Playground</h2>



<p class="wp-block-paragraph">You do not need a full WordPress installation to test this. The <a href="https://wordpress.github.io/wordpress-playground/developers/local-development/wp-playground-cli/">Playground CLI</a> gives you a disposable WordPress instance in seconds. Make sure you have Node.js 20.18 or later, then from the plugin directory run:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">npm install
npm run build
npx @wp-playground/cli@latest server --auto-mount --login</code></pre>



<p class="wp-block-paragraph">Playground detects the plugin, automatically mounts it and logs in the admin user. Open <code>http://127.0.0.1:9400</code> in your browser, create or edit a post, and you should see “Social Card Preview” in the Preview dropdown.</p>



<h2 class="wp-block-heading" id="going-further">Going further</h2>



<p class="wp-block-paragraph">The social card example is one way to use <code>PluginPreviewMenuItem</code>. The slot opens up a range of preview experiences that were previously only available to WordPress core. Here are some other use cases to consider:</p>



<ul class="wp-block-list">
<li><strong>Accessibility checker</strong> — open a modal that scans the post content for common accessibility issues, such as missing alt text or low-contrast headings, before the author hits publish.</li>



<li><strong>Reading level preview</strong> — show a readability score and a simplified version of the content, useful for publishers targeting a broad or non-specialist audience.</li>



<li><strong>External preview service</strong> — use the <code>href</code> prop instead of <code>onClick</code> to send the author directly to a third-party staging or QA environment with the post URL pre-filled.</li>



<li><strong>Email newsletter preview</strong> — for plugins that sync posts to an email list, show a rendered preview of how the content will look in an email client, including any template wrapping applied by the plugin.</li>
</ul>



<p class="wp-block-paragraph">Any time your plugin needs to give authors a way to see or check their content before publishing, <code>PluginPreviewMenuItem</code> is the right place to add it.</p>



<p class="has-text-align-right wp-block-paragraph"><em>Props to </em><a class="mention" href="https://profiles.wordpress.org/greenshady/"><span class="mentions-prefix">@</span>greenshady</a><em>and </em><a class="mention" href="https://profiles.wordpress.org/juanmaguitar/"><span class="mentions-prefix">@</span>juanmaguitar</a> <em>for reviews.</em></p>

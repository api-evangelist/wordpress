---
title: "What’s new for developers? (March 2026)"
url: "https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/"
date: "Tue, 10 Mar 2026 15:03:54 +0000"
author: "Birgit Pauli-Haack"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">The release cycle for WordPress 7.0 is rapidly advancing. The latest <a href="https://make.wordpress.org/core/2026/02/25/whats-new-in-gutenberg-22-6-25-february/">Gutenberg release (22.6)</a> has rounded up the features slated for 7.0, and the Release Candidate (RC1) is scheduled for March 19, 2026. The official Field Guide is also currently in development. <a href="https://wordpress.org/news/2026/03/wordpress-7-0-beta-3/">WordPress 7.0 Beta 3</a> is now available for testing. The test team encourages participation and has published <a href="https://make.wordpress.org/test/2026/02/20/help-test-wordpress-7-0/">a helpful guide</a>, including summaries and videos, to help users become familiar with the new features.</p>



<p class="wp-block-paragraph">Make sure you update immediately to the security-only minor release <a href="https://wordpress.org/news/2026/03/wordpress-6-9-2-release/">WordPress 6.9.2</a> from today (10 March).  It patches ten vulnerabilities: a blind SSRF, a PoP-chain weakness in the HTML API and Block Registry, regex DoS in numeric character references, stored XSS in nav menus and via the <code>data-wp-bind</code> directive, an AJAX authorization bypass, a PclZip path traversal, and an XXE in the bundled getID3 library—now also patched upstream. </p>



<p class="wp-block-paragraph"><strong>Update March 12:</strong> In the meantime <a href="https://wordpress.org/news/2026/03/wordpress-6-9-3-and-7-0-beta-4/">WordPress 6.9.3 + 7.0 Beta 4</a>, and then <a href="https://wordpress.org/news/2026/03/wordpress-6-9-4-release/">version 6.9.4</a> were released. </p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#highlights">Highlights</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#real-time-collaboration-rtc-coming-to-wordpress-7-0">Real-time Collaboration (RTC)  coming to WordPress 7.0 </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#ai-provider-packages-in-the-plugin-directory">AI provider packages in the plugin directory</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#in-editor-revisions-visual-change-tracking">In-Editor revisions: visual change tracking</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#plugins-and-tools">Plugins and tools</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#iframed-post-editor-punted-wordpress-7-1">Iframed post editor punted WordPress 7.1 </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#new-wp-cli-wp-block-and-ability-commands">New WP CLI wp block and ability commands</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#phpmyadmin-support-in-wp-env-playground-runtime">phpMyAdmin support in wp-env Playground runtime</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#global-styles-custom-css-now-honors-block-defined-feature-selectors">Global Styles custom CSS now honors block-defined feature selectors</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#work-on-ui-package-and-components-continues">Work on UI package and components continues</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#themes">Themes</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#icon-block">Icon block</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#navigation-overlays-patterns">Navigation overlays patterns </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#contentonly-pattern-editing">ContentOnly pattern editing </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#gallery-lightbox-now-supports-image-navigation">Gallery lightbox now supports image navigation</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#text-align-support-expanded">Text align support expanded </a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#resources">Resources</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#first-dev-notes-for-wordpress-7-0">First Dev Notes for WordPress 7.0 </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#developer-blog">Developer blog</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#external-tools">External tools</a></li></ol></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="highlights">Highlights</h2>



<h3 class="wp-block-heading" id="real-time-collaboration-rtc-coming-to-wordpress-7-0">Real-time Collaboration (RTC)&nbsp; coming to WordPress 7.0&nbsp;</h3>



<p class="wp-block-paragraph">The underlying technical plumbing for RTC is now solved ahead of Beta 4. The implementation uses an HTTP polling sync provider, replacing unreliable WebRTC for universal compatibility across hosting environments. CRDT (Conflict-free Replicated Data Type) update data is stored persistently using post_meta on a special internal post type (<code>wp_sync_storage</code>). The sync provider architecture is designed so that the storage and transport layer can be swapped out. Updates are periodically compacted, and requests are batched. Client-side Gutenberg code initially limits simultaneous collaborators to two, but hosts can add a different provider or adjust defaults via a wp-config constant. The decision to enable RTC by default will be finalized around RC2. See also the <a href="https://make.wordpress.org/core/2026/03/10/real-time-collaboration-in-the-block-editor/">accompanying Dev Note</a>. </p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Screenshot of real-time collaborative editing" class="wp-image-5943" height="624" src="https://developer.wordpress.org/news/files/2026/03/image-1.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="ai-provider-packages-in-the-plugin-directory">AI provider packages in the plugin directory</h3>



<p class="wp-block-paragraph">WordPress 7.0 will introduce a Connector feature built around the <a href="https://packagist.org/packages/wordpress/php-ai-client">php-ai-client package</a>, a shared PHP library for standard AI service communication. Three provider packages are now available in the Plugin Directory: one each for <a href="https://wordpress.org/plugins/openai-provider/">OpenAI</a>, <a href="https://wordpress.org/plugins/google-ai-provider/">Google</a>, and <a href="https://wordpress.org/plugins/anthropic-ai-provider/">Anthropic</a>. This structure allows developers to write features once against the shared interface, making provider switching a simple configuration change.<br />The <a href="https://github.com/WordPress/gutenberg/pull/75833">Connectors screen</a> will land in Core, establishing credentials storage and provider selection as platform-level infrastructure.</p>



<figure class="wp-block-image size-large wp-lightbox-container"><img alt="Screenshot of new Connectors screen" class="wp-image-5946" height="573" src="https://developer.wordpress.org/news/files/2026/03/image-1024x573.jpeg" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="in-editor-revisions-visual-change-tracking">In-Editor revisions: visual change tracking</h3>



<p class="wp-block-paragraph">The block editor&#8217;s revisions panel now offers a <a href="https://github.com/WordPress/gutenberg/pull/75049">visual way to track changes</a> directly in the document inspector. Color-coded overlays indicate changes: green outlines for added blocks, red for removed blocks, and yellow for blocks with modified settings. For text content, added text is green/underlined, removed text is red/Strikethrough, and format-only changes receive a yellow outline. This overlay can be toggled off. The feature uses a two-step process—a quick check for changed blocks, followed by a full rich-text comparison only on flagged blocks—and uses currentColor for theme-compatible coloring.</p>



<figure class="wp-block-image size-large wp-lightbox-container"><img alt="In-editor revisions screen" class="wp-image-5947" height="624" src="https://developer.wordpress.org/news/files/2026/03/image-2-1024x624.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h2 class="wp-block-heading" id="plugins-and-tools">Plugins and tools</h2>



<p class="wp-block-paragraph">Several Dev Notes have been published to give developers and agencies time to prepare for the new version. (see <a href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#first-dev-notes-for-wordpress-7-0">Ressources section</a>) The final list of Dev notes will be published with the Field Guide after Release Candidate1. </p>



<h3 class="wp-block-heading" id="iframed-post-editor-punted-wordpress-7-1">Iframed post editor punted WordPress 7.1&nbsp;</h3>



<p class="wp-block-paragraph">The &#8220;Always-iframed post editor,&#8221; covered in <a href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#always-iframed-post-editor">What’s new for Developer (February 2026)</a>, has been punted to Core WordPress 7.1. However, the Gutenberg plugin will still iframe the post editor blocks. <a href="https://make.wordpress.org/core/2026/02/24/iframed-editor-changes-in-wordpress-7-0/">More details are available</a>.</p>



<h3 class="wp-block-heading" id="new-wp-cli-wp-block-and-ability-commands">New WP CLI wp block and ability commands</h3>



<p class="wp-block-paragraph">The WP-CLI team is developing a new set of commands (<code>wp block</code>) for read-only access to block entities, with an exception for exporting patterns and templates. An additional set of <a href="https://developer.wordpress.org/cli/commands/ability/">ability commands</a> is also in development. These packages are ahead of WP-CLI v3.0 and available as dev dependencies for testing:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">wp package install wp-cli/block-command:dev-main
wp package install wp-cli/ability-command:dev-main 
</code></pre>



<p class="wp-block-paragraph">Or via Composer&nbsp;</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">composer require wp-cli/block-command:dev-main --dev
composer require wp-cli/ability-command:dev-main --dev</code></pre>



<p class="wp-block-paragraph">or you could just use: </p>



<pre class="wp-block-code"><code class="">wp cli update --nightly</code></pre>



<p class="wp-block-paragraph">The team is targeting a 3.0 stable release for the end of March.</p>



<h3 class="wp-block-heading" id="phpmyadmin-support-in-wp-env-playground-runtime">phpMyAdmin support in wp-env Playground runtime</h3>



<p class="wp-block-paragraph">The wp-env Playground runtime now <a href="https://github.com/WordPress/gutenberg/pull/75532">supports phpMyAdmin</a>, reaching feature parity with the Docker runtime. You can enable it by adding a boolean options to your <code>.wp-env.json</code> configuration.</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
&nbsp; &nbsp; "phpmyadmin": true,
&nbsp; &nbsp; "runtime": "playground"
}</code></pre>



<p class="wp-block-paragraph">When enabled, phpMyAdmin is accessible at <code>http://localhost:8888/phpmyadmin</code>, and wp-env status will display the URL.&nbsp;</p>



<h3 class="wp-block-heading" id="global-styles-custom-css-now-honors-block-defined-feature-selectors">Global Styles custom CSS now honors block-defined feature selectors</h3>



<p class="wp-block-paragraph">The block selectors API, which allows block authors to define feature-specific CSS targets in <code>block.json</code>, is now honored by the &#8220;<a href="https://github.com/WordPress/gutenberg/pull/75799">Additional CSS&#8221; feature in Global Styles</a>. This change allows a block to declare a selectors.css entry in its block.json to point custom CSS at a specific inner element (e.g., inner content, an image, or an &lt;svg&gt;), giving precise control over theme-level custom CSS.Work on UI and Components Continues</p>



<h3 class="wp-block-heading" id="work-on-ui-package-and-components-continues">Work on UI package and components continues</h3>



<p class="wp-block-paragraph">The UI package continues to be developed with additional primitives and features, <a href="https://github.com/WordPress/gutenberg/issues/71196">supporting the Admin redesign</a>. Components recently added include:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/74697">IconButton component</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75133">Add a minimum switch</a> to the Button component&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74707">Textarea primitive component&nbsp;</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74652">Tabs component</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75183">Dialog component </a>&nbsp;</li>
</ul>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/74557">Use semantic dimension tokens</a>.</p>



<h2 class="wp-block-heading" id="themes">Themes</h2>



<h3 class="wp-block-heading" id="icon-block">Icon block</h3>



<p class="wp-block-paragraph">Designers can now utilize <a href="https://github.com/WordPress/gutenberg/pull/71227">a new Icon block</a> to add SVG icons from a pre-selected library. This is backed by the new server-side SVG Icon Registration API. A REST endpoint is available at <code>/wp/v2/icons</code> for searching and filtering. The initial doesn&#8217;t allow registering third-party icon collections and draws from the <code>wordpress/icons</code> package. Extensibility for third-party icon registration is planned for the future, likely in 7.1, following further development on the Icon registry API architecture. The initial set draws from the <code>wordpress/icons</code> package.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Icon blocks in a location screen. " class="wp-image-5952" height="226" src="https://developer.wordpress.org/news/files/2026/03/image-3-1.png" width="766" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="navigation-overlays-patterns">Navigation overlays patterns&nbsp;</h3>



<p class="wp-block-paragraph">Navigation blocks now feature customizable overlays, giving users full control over mobile menus. The feature is no longer experimental and will ship with WordPress 7.0. A <strong>Create overlay</strong> button guides the setup, offering patterns for various designs.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Navigation overlays pattern in block editor " class="wp-image-5955" height="498" src="https://developer.wordpress.org/news/files/2026/03/image-4-1.png" width="768" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">The details are available in the following PRs:&nbsp;</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/74968#top">Remove experiment</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74971#top">Add Create Overlay button</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75564#top">Update overlay template part naming to &#8216;Navigation Overlay&#8217;</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75276#top">Filter navigation category patterns to only show in navigation-overlay template part context</a></li>
</ul>



<h3 class="wp-block-heading" id="contentonly-pattern-editing">ContentOnly pattern editing&nbsp;</h3>



<p class="wp-block-paragraph">For WordPress 7.0,&nbsp; Patterns now default to <a href="https://github.com/WordPress/gutenberg/issues/73775">Content-Only editing mode</a>. This mode presents fields organized with block icons and grouped attributes in flyout menus, reducing design clutter for content creators. Rich text formatting works inline without interruption from the toolbar. When structural edits are needed, detaching a pattern restores full block access. </p>



<p class="wp-block-paragraph">Administrators can opt out of Content-Only mode for unsynced patterns using the new <code>disableContentOnlyForUnsyncedPatterns</code> setting via PHP filter or JavaScript dispatch.</p>



<pre class="wp-block-code"><code class="language-php" lang="php">add_filter( 'block_editor_settings_all', function( $settings ) {
    $settings['disableContentOnlyForUnsyncedPatterns'] = true;
    return $settings;
} );
</code></pre>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">wp.data.dispatch( 'core/block-editor' ).updateSettings( {
    disableContentOnlyForUnsyncedPatterns: true,
} );
</code></pre>



<h3 class="wp-block-heading" id="gallery-lightbox-now-supports-image-navigation">Gallery lightbox now supports image navigation</h3>



<p class="wp-block-paragraph">The lightbox feature in the Gallery block has been <a href="https://github.com/WordPress/gutenberg/pull/62906">extended to support navigation</a> between images using back/next buttons and arrow keys. Images with lightbox disabled are automatically skipped.</p>



<figure class="wp-block-image size-large wp-lightbox-container"><img alt="Gallery lightbox navigation" class="wp-image-5957" height="757" src="https://developer.wordpress.org/news/files/2026/03/image-5-1024x757.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="text-align-support-expanded">Text align support expanded&nbsp;</h3>



<p class="wp-block-paragraph">Eight blocks have been migrated to the standardized text-align block support:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/74997">Author Biography</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75109">Post Author Name</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75321">Post Comments Count</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75322">Post Comments Form</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75332">Post Comments Link</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75545">Post Terms</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75541">Post Time to Read</a>&nbsp;</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/75542">Term Description</a>&nbsp;</li>
</ul>



<h2 class="wp-block-heading" id="resources">Resources</h2>



<h3 class="wp-block-heading" id="first-dev-notes-for-wordpress-7-0">First Dev Notes for WordPress 7.0 </h3>



<ul class="wp-block-list">
<li><a href="https://make.wordpress.org/core/2026/03/04/breadcrumb-block-filters/">Breadcrumb block filters</a>: Learn how to use the two new PHP filters to customize breadcrumb trail items and taxonomy/term preferences.</li>



<li><a href="https://make.wordpress.org/core/2026/03/04/customisable-navigation-overlays-in-wordpress-7-0/">Customizable Navigation Overlays</a>:&nbsp; Theme developers learn how to register and bundle the new navigation-overlay template part area for fully customizable mobile navigation overlays.</li>



<li><a href="https://make.wordpress.org/core/2026/03/04/changes-to-the-interactivity-api-in-wordpress-7-0/">Changes to the Interactivity API</a>: The new `watch()` function and server-side `state.url` population enable cleaner patterns for side effects and navigation tracking. Note that `state.navigation` is now deprecated.</li>



<li><a href="https://make.wordpress.org/core/2026/03/04/dataviews-dataform-et-al-in-wordpress-7-0/">DataViews, DataForm, et al. </a>: A substantial API update introduces new layouts, validation rules, grouping options, and picker improvements affecting plugins using `wordpress/dataviews`.</li>



<li><a href="https://make.wordpress.org/core/2026/03/03/php-only-block-registration/">PHP-only block registration</a>: You can now register a fully functional block with only PHP using the new `autoRegister` support flag—no JavaScript required.&nbsp;</li>



<li><a href="https://make.wordpress.org/core/2026/03/09/pseudo-element-support-for-blocks-and-their-variations-in-theme-json/">Pseudo-element support for blocks and their variations in theme.json</a>: Theme developers can now style :hover, :focus, :focus-visible, and :active states directly on blocks and their style variations in theme.json, removing the need for custom CSS.</li>



<li><a href="https://make.wordpress.org/core/2026/03/10/real-time-collaboration-in-the-block-editor/">Real-Time Collaboration in the Block Editor</a>: Essential reading for plugin developers: learn how classic meta boxes disable collaboration mode, how to use the sync.providers filter to customize the Yjs transport layer, and how to avoid common pitfalls like local state drift and unintended block insertion side effects.</li>
</ul>



<h3 class="wp-block-heading" id="developer-blog">Developer blog</h3>



<p class="wp-block-paragraph">Two new blog posts landed on the Developer Blog in the past month. If you haven’t read them already, now’s the time:</p>



<ul class="wp-block-list">
<li><a href="https://developer.wordpress.org/news/2026/02/a-better-way-to-test-html-in-wordpress-with-assertequalhtml/">A better way to test HTML in WordPress with assertEqualHTML()</a></li>



<li><a href="https://developer.wordpress.org/news/2026/02/how-to-add-custom-entries-to-the-editor-preview-dropdown/">How to add custom entries to the editor Preview dropdown</a></li>
</ul>



<p class="wp-block-paragraph">Never want to miss an article again? <a href="https://developer.wordpress.org/news/subscribe/">Subscribe to the WordPress Developer Blog</a></p>



<h3 class="wp-block-heading" id="external-tools">External tools</h3>



<p class="wp-block-paragraph"><a href="http://yjs.dev/">Yjs</a> is the engine powering WordPress&#8217;s long-awaited real-time collaborative editing.</p>



<p class="has-text-align-right wp-block-paragraph"><em>Props to&nbsp;<a class="mention" href="https://profiles.wordpress.org/greenshady/"><span class="mentions-prefix">@</span>greenshady</a> and <a class="mention" href="https://profiles.wordpress.org/psykro/"><span class="mentions-prefix">@</span>psykro</a> for reviewing this article.</em></p>



<p class="wp-block-paragraph"></p>

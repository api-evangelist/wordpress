---
title: "What’s new for developers? (February 2026)"
url: "https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/"
date: "Tue, 10 Feb 2026 18:18:12 +0000"
author: "Justin Tadlock"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">WordPress 7.0 Beta 1 is fast approaching. That means the mad rush to get everything into Gutenberg and Core before the February 19th deadline is in full swing. The last couple of Gutenberg releases (22.4 and 22.5) shipped with a ton of new features.</p>



<p class="wp-block-paragraph">And, as always, the monthly roundup is available to help you catch up.</p>



<p class="wp-block-paragraph">In other news, <a href="https://wordpress.org/news/2026/02/wordpress-6-9-1-maintenance-release/">WordPress 6.9.1</a> shipped on February 3, 2026 with 49 bug fixes. If you haven’t done so already, be sure to upgrade to the latest version.</p>



<p class="wp-block-paragraph">Now, let’s get back to upcoming features. Be sure to test with WordPress trunk and the latest version of the Gutenberg plugin active. You can also <a href="https://playground.wordpress.net/?wp=nightly&amp;plugin=gutenberg">test the latest updates via Playground</a>.</p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#highlights">Highlights</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#always-iframed-post-editor">Always-iframed post editor</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#viewport-based-block-visibility">Viewport-based block visibility</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#per-block-instance-custom-css">Per-block instance custom CSS</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#plugins-tools">Plugins &amp; Tools</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#wordpress-studio-cli-updates">WordPress Studio CLI updates</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#ai-and-agent-features">AI and agent features</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#ui-primitives-and-components">UI Primitives and Components</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#anchor-support-for-dynamic-blocks">Anchor support for dynamic blocks</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#themes">Themes</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#text-supports-improved-for-multiple-blocks">Text supports improved for multiple blocks</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#ai-generated-images-allowed-in-theme-directory">AI-generated images allowed in theme directory</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#default-link-styles-removed">Default link styles removed</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#breadcrumbs-block-updates">Breadcrumbs block updates</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#extra-divs-removed-from-blocks-in-the-editor">Extra divs removed from blocks in the editor</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#gallery-caption-background-blur">Gallery caption background blur</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#pullquote-block-reinstated">Pullquote block reinstated</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#aspect-ratios-for-image-blocks-at-all-alignments">Aspect ratios for Image blocks at all alignments</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#tabs-block-restructured">Tabs block restructured</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#navigation-and-overlays">Navigation and overlays</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#other-notable-block-changes">Other notable block changes</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#playground">Playground</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#notable-user-facing-changes">Notable user-facing changes</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#resources">Resources</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/#developer-blog">Developer Blog</a></li></ol></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="highlights">Highlights</h2>



<h3 class="wp-block-heading" id="always-iframed-post-editor">Always-iframed post editor</h3>



<div class="wp-block-wporg-notice is-alert-notice"><div class="wp-block-wporg-notice__icon"></div><div class="wp-block-wporg-notice__content"><p>This has changed since this post was published. The post editor will always be iframed unless there is a block inserted into the content with an API version lower than 3. For more information, read <a href="https://make.wordpress.org/core/2026/02/24/iframed-editor-changes-in-wordpress-7-0/">Iframed Editor Changes in WordPress 7.0</a>.</p></div></div>



<p class="wp-block-paragraph">For several years, every block-based editor has existed in an iframe. This has had the benefit of separating UI styles from block and theme styles. However, blocks using version 2 of the block API triggered the post editor (but not the template and site editors) to use the old non-iframed editor. This has led to an inconsistent experience for users and extenders.</p>



<p class="wp-block-paragraph">In WordPress 7.0, the post editor will always be iframed, regardless of the API version of the block.</p>



<p class="wp-block-paragraph">For the most part, this should not negatively impact the user experience. However, there are potential edge cases where some blocks may rely on the global document in JavaScript or CSS that may need to be updated.</p>



<p class="wp-block-paragraph">The reasons for this change were <a href="https://make.wordpress.org/core/2021/06/29/blocks-in-an-iframed-template-editor/">announced nearly five years ago</a> and <a href="https://make.wordpress.org/core/2025/11/12/preparing-the-post-editor-for-full-iframe-integration/">reiterated prior to the WordPress 6.9 release</a>. To ensure your blocks are updated and working correctly, check out the <a href="https://developer.wordpress.org/block-editor/reference-guides/block-api/block-api-versions/block-migration-for-iframe-editor-compatibility/">migration guide in the handbook</a>.</p>



<h3 class="wp-block-heading" id="viewport-based-block-visibility">Viewport-based block visibility</h3>



<figure class="wp-block-image alignwide size-full has-custom-border wp-lightbox-container"><img alt="WordPress post editor with a full-screen Cover block in the background. A modal is popped up showing various options for hiding the block." class="has-border-color has-light-grey-1-border-color wp-image-5846" height="1106" src="https://developer.wordpress.org/news/files/2026/02/block-visibility-viewport.webp" style="border-width: 1px;" width="2048" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">The Block Visibility feature landed in WordPress 6.9 with the ability to hide a block from appearing on the front end. Version 7.0 is slated to include <a href="https://github.com/WordPress/gutenberg/pull/74839">viewport-based visibility controls</a>, building up that initial foundation.</p>



<p class="wp-block-paragraph">To follow along with the progress of both the UI and the underlying code, check out these tickets:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/74602">Refactor metadata to use nested structure</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74517">Create selectors for block visibility in current viewport</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74679">Render blocks when hidden at all viewports</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74379">Add rules to hide on viewport size</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74249">Add viewport modal and controls UI</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74180">Add visibility notice for hidden blocks in the block inspector</a></li>
</ul>



<h3 class="wp-block-heading" id="per-block-instance-custom-css">Per-block instance custom CSS</h3>



<figure class="wp-block-image alignwide size-full has-custom-border wp-lightbox-container"><img alt="WordPress post editor with a Group block selected. In the sidebar, an Additional CSS box shows a lot of custom CSS." class="has-border-color has-light-grey-1-border-color wp-image-5847" height="1106" src="https://developer.wordpress.org/news/files/2026/02/additional-css.webp" style="border-width: 1px;" width="2048" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">Gutenberg 22.5 brings custom CSS <a href="https://github.com/WordPress/gutenberg/pull/73959">support to individual block instances</a>. Under the <strong>Advanced <span class="wp-exclude-emoji">→</span> Additional CSS</strong> block sidebar control, you can add CSS specific to that single instance of a block. A <code>.has-custom-css</code> <a href="https://github.com/WordPress/gutenberg/pull/74969">CSS class is also added</a> dynamically in both the editor and on the front end when a block has CSS.</p>



<p class="wp-block-paragraph">This feature is one of those double-edged swords, being both useful for one-off changes and also creating later management headaches. There’s an open <a href="https://github.com/WordPress/gutenberg/issues/75236">ticket discussing an indicator</a> when a block has custom CSS attached to it. In most cases, you’ll likely want to rely on keeping your styles at the global level or use block style variations to keep your code base cleaner.</p>



<h2 class="wp-block-heading" id="plugins-tools">Plugins &amp; Tools</h2>



<h3 class="wp-block-heading" id="wordpress-studio-cli-updates">WordPress Studio CLI updates</h3>



<p class="wp-block-paragraph"><a href="https://github.com/Automattic/studio/releases/tag/v1.7.0">Version 1.7.0</a> of WordPress Studio saw substantial updates to its command line tools. You can now control nearly every feature—other than Sync—directly from the command lines. This means that it will work well with AI-assisted development tools, such as Claude Code and Cursor.</p>



<h3 class="wp-block-heading" id="ai-and-agent-features">AI and agent features</h3>



<p class="wp-block-paragraph">The <a href="https://wordpress.org/plugins/ai/">AI Experiments plugin</a> has been updated to add several improvements:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/ai/pull/96">Excerpt Generation</a>:&nbsp; AI-powered post summaries now integrate directly with WordPress, with an <a href="https://github.com/WordPress/ai/pull/143">experimental editor interface</a> for generating excerpts.</li>



<li><a href="https://github.com/WordPress/ai/pull/63">Abilities Explorer</a>: New admin screen that shows all registered AI capabilities in one place, letting you view and test available features.</li>



<li><a href="https://github.com/WordPress/ai/pull/136">Content Summarization</a> and <a href="https://github.com/WordPress/ai/pull/134">Image Generation</a>: Backend API support added for these experiments (there’s no UI yet, but the foundation is ready).</li>



<li><a href="https://github.com/WordPress/ai/pull/135">Improved Documentation</a>: Expanded readme with better onboarding content and clearer setup instructions.</li>



<li><a href="https://github.com/WordPress/ai/pull/144">Playground Preview</a>: Automated preview builds for testing changes directly in WordPress Playground.</li>
</ul>



<h3 class="wp-block-heading" id="ui-primitives-and-components">UI Primitives and Components</h3>



<p class="wp-block-paragraph">The WordPress UI package received a significant update with the addition of several components and primitives designed to help developers build more consistent and accessible interfaces:&nbsp;</p>



<ul class="wp-block-list">
<li>A new dropdown/select menu component for creating <a href="https://github.com/WordPress/gutenberg/pull/74661">standardized select controls</a>.</li>



<li>A <a href="https://github.com/WordPress/gutenberg/pull/74625">tooltip component</a> for displaying helpful hints when users hover over elements.</li>



<li>The building blocks for <a href="https://github.com/WordPress/gutenberg/pull/74190">creating form fields</a> with consistent styling and behavior.</li>



<li>A component that hides content <a href="https://github.com/WordPress/gutenberg/pull/74189">from visual display</a> while keeping it accessible to assistive technologies.</li>



<li>A <a href="https://github.com/WordPress/gutenberg/pull/74415">standardized button component</a> for creating consistent interactive elements.</li>



<li>Building blocks for grouping <a href="https://github.com/WordPress/gutenberg/pull/74296">related form controls</a> together (fieldsets).</li>



<li>A component for <a href="https://github.com/WordPress/gutenberg/pull/74311">displaying icons</a> consistently throughout your WordPress interface.</li>



<li>A building block for creating consistent <a href="https://github.com/WordPress/gutenberg/pull/74313">layouts around input fields</a>.</li>



<li>A basic building block for <a href="https://github.com/WordPress/gutenberg/pull/74615">creating text input fields</a> with standardized appearance and functionality.</li>
</ul>



<h3 class="wp-block-heading" id="anchor-support-for-dynamic-blocks">Anchor support for dynamic blocks</h3>



<p class="wp-block-paragraph">Anchor (<code>id</code> attribute) support now <a href="https://github.com/WordPress/gutenberg/pull/74183">works for dynamic blocks</a>. The reference is always saved in the block comment delimiter, which allows it to be rendered on the front end dynamically. The change also updates most dynamic Core blocks to include support.</p>



<h2 class="wp-block-heading" id="themes">Themes</h2>



<h3 class="wp-block-heading" id="text-supports-improved-for-multiple-blocks">Text supports improved for multiple blocks</h3>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/74383">Heading</a>, <a href="https://github.com/WordPress/gutenberg/pull/74724">Verse</a>, and several comment-related blocks (<a href="https://github.com/WordPress/gutenberg/pull/74068">Author Name</a>, <a href="https://github.com/WordPress/gutenberg/pull/74269">Content</a>, <a href="https://github.com/WordPress/gutenberg/pull/74599">Date</a>, <a href="https://github.com/WordPress/gutenberg/pull/74720">Edit Link</a>, <a href="https://github.com/WordPress/gutenberg/pull/74760">Reply Link</a>, and <a href="https://github.com/WordPress/gutenberg/pull/74945">Title</a>) now fully support the <code>textAlign</code> feature. During the 7.0 cycle, contributors standardized text alignment and have been updating blocks across the board. Follow the <a href="https://github.com/WordPress/gutenberg/issues/60763">migration ticket</a> to follow along.</p>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/73114">Text indent support was added</a> in an initial pull request to get the long-requested indentation feature added to the Block Editor. The current style is limited to a specific type of indentation (first paragraph not indented but subsequent ones are). The initial implementation lacked enough cross-language support, and more <a href="https://github.com/WordPress/gutenberg/pull/74889">options for handling indentation</a> will land in Gutenberg 22.6.</p>



<p class="wp-block-paragraph">The Paragraph block also gained <code>textColumns</code> support, which allows you to turn a single paragraph into <a href="https://github.com/WordPress/gutenberg/pull/74656">multiple columns of text</a>.</p>



<h3 class="wp-block-heading" id="ai-generated-images-allowed-in-theme-directory">AI-generated images allowed in theme directory</h3>



<p class="wp-block-paragraph">A discussion kicked off last year over whether AI-generated images could be bundled with themes in the directory. Eventually, WordPress Executive Director Mary Hubbard <a href="https://themes.trac.wordpress.org/ticket/234012#comment:24">advised to move forward</a> with their allowance:</p>



<blockquote class="wp-block-quote has-large-font-size is-layout-flow wp-block-quote-is-layout-flow">
<p class="wp-block-paragraph">AI-generated images can be used if they are explicitly disclosed and licensed in a GPL-compatible way. If the author declares this, I don&#8217;t see an issue in moving it forward.</p>
</blockquote>



<p class="wp-block-paragraph">The Themes Team solidified that decision during its <a href="https://make.wordpress.org/themes/2026/01/27/themes-team-meeting-agendas-for-january-27-2026/">January 27, 2026 team meeting</a>.</p>



<h3 class="wp-block-heading" id="default-link-styles-removed">Default link styles removed</h3>



<p class="wp-block-paragraph">Previously, the default WordPress <code>theme.json</code> file added an underline as the default text-decoration on link elements. Since this is already the browser default, it was redundant. This <a href="https://github.com/WordPress/gutenberg/pull/74901">has now been removed</a> and should not impact most themes, but it’s worth checking just to be sure.</p>



<h3 class="wp-block-heading" id="breadcrumbs-block-updates">Breadcrumbs block updates</h3>



<p class="wp-block-paragraph">The Breadcrumbs block is still receiving some fine-tuning as it gears up for the WordPress 7.0 release. The latest changes include:</p>



<ul class="wp-block-list">
<li><code>theme.json</code> <a href="https://github.com/WordPress/gutenberg/pull/74227">block schema support</a></li>



<li>Applies <code>post_type_archive_title</code> filters when showing <a href="https://github.com/WordPress/gutenberg/pull/73966">the post type archive title</a></li>



<li>A new <code>block_core_breadcrumbs_items</code> <a href="https://github.com/WordPress/gutenberg/pull/74169">filter hook</a> for overwriting the final array</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74170">Passes the post ID</a> as an argument to the existing <code>block_core_breadcrumbs_post_type_settings</code> hook</li>
</ul>



<h3 class="wp-block-heading" id="extra-divs-removed-from-blocks-in-the-editor">Extra divs removed from blocks in the editor</h3>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/74228">Gutenberg 22.4 introduced</a> a new <code>HtmlRenderer</code> component, which renders HTML content as React elements with optional wrapper props. For theme authors, this means that several blocks will no longer have an extra wrapping <code>&lt;div&gt;</code> in the editor, allowing for consistent styling with the front end.</p>



<p class="wp-block-paragraph">Blocks which have now been fixed are:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/74255">Archives</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74271">Calendar</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74277">Latest Comments</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74272">RSS</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74228">Tag Cloud</a></li>
</ul>



<h3 class="wp-block-heading" id="gallery-caption-background-blur">Gallery caption background blur</h3>



<p class="wp-block-paragraph">The <a href="https://github.com/WordPress/gutenberg/pull/74063">caption background blur</a> for Gallery Image captions has been changed from a max height of <code>40%</code> to <code>3em</code>. This could impact custom styles, so be sure to check its output with your theme.</p>



<p class="wp-block-paragraph">The original proposal was to move the background to the <code>&lt;figcaption&gt;</code> element itself, but that proved problematic with some image dimensions.</p>



<h3 class="wp-block-heading" id="pullquote-block-reinstated">Pullquote block reinstated</h3>



<p class="wp-block-paragraph">The Pullquote block was <a href="https://github.com/WordPress/gutenberg/pull/73228">deprecated in Gutenberg 22.2</a> in favor of pushing users toward the Quote block. However, after a <a href="https://github.com/WordPress/gutenberg/issues/11610">lengthy discussion</a> with lots of community feedback, contributors realized these two blocks are semantically different and are for entirely different use cases. The <a href="https://github.com/WordPress/gutenberg/pull/75122%5C">block has been reinstated</a> with no plans for deprecation as of now.</p>



<p class="wp-block-paragraph">There is still an <a href="https://github.com/WordPress/gutenberg/issues/20606">ongoing discussion</a> to address the Quote and Pullquote block’s markup and ensure they are semantically valid HTML and accessible.</p>



<h3 class="wp-block-heading" id="aspect-ratios-for-image-blocks-at-all-alignments">Aspect ratios for Image blocks at all alignments</h3>



<p class="wp-block-paragraph">In WordPress 6.9 and earlier, you were unable to define an aspect ratio for an Image block when it was set to wide or full alignment. This meant registering custom image sizes (technically, <em>resolutions</em>) and using them as <em>faux</em> aspect ratios. In WordPress 7.0, you’ll be able to correctly set wide and full-width images <a href="https://github.com/WordPress/gutenberg/pull/74519">to any registered aspect ratio</a>.</p>



<h3 class="wp-block-heading" id="tabs-block-restructured">Tabs block restructured</h3>



<p class="wp-block-paragraph">The Tabs block has undergone a <a href="https://github.com/WordPress/gutenberg/pull/74412">significant refactoring</a> based on feedback from Core contributors. The block now has multiple inner blocks, giving you much more control over styling its output.</p>



<p class="wp-block-paragraph">The outer Tabs block now has a nested structure:</p>



<ul class="wp-block-list">
<li>Tabs Menu
<ul class="wp-block-list">
<li>Tabs Menu Item</li>
</ul>
</li>



<li>Tab Panels
<ul class="wp-block-list">
<li>Tab</li>
</ul>
</li>
</ul>



<p class="wp-block-paragraph">The change also removes the Button and Link styles present in earlier versions. This will make it easier for you if you were previously disabling those styles or restyling them to match your design.</p>



<h3 class="wp-block-heading" id="navigation-and-overlays">Navigation and overlays</h3>



<p class="wp-block-paragraph">The Navigation Overlay feature continues to improve. The last two Gutenberg releases added several important updates and fixes:</p>



<ul class="wp-block-list">
<li><a href="https://github.com/WordPress/gutenberg/pull/74780">Sidebar previews</a> for overlays.</li>



<li><a href="https://github.com/WordPress/gutenberg/pull/74650">Default pattern inserted</a> on overlay creation, which now <a href="https://github.com/WordPress/gutenberg/pull/74659">has a background</a>.</li>



<li>Updated <a href="https://github.com/WordPress/gutenberg/pull/74690">control labels</a>.</li>



<li>New Navigation blocks now default to <a href="https://github.com/WordPress/gutenberg/pull/74890">always show overlays</a>.</li>



<li>New overlay patterns for <a href="https://github.com/WordPress/gutenberg/pull/74861">centered navigation</a>, <a href="https://github.com/WordPress/gutenberg/pull/74862">centered nav with info</a>, <a href="https://github.com/WordPress/gutenberg/pull/74849">with accent background</a>, and <a href="https://github.com/WordPress/gutenberg/pull/74847">with black background</a>.</li>



<li>Navigation blocks within overlays <a href="https://github.com/WordPress/gutenberg/pull/74764">no longer use</a> a <code>&lt;nav&gt;</code> tag.</li>



<li>Submenu colors are no longer <a href="https://github.com/WordPress/gutenberg/pull/74544">applied to custom overlays</a>.</li>



<li>Themes can define the overlay attribute <a href="https://github.com/WordPress/gutenberg/pull/74119">without the theme slug</a>.</li>



<li>The Navigation block has a new option to <a href="https://github.com/WordPress/gutenberg/pull/74653">always toggle submenus open</a>.</li>
</ul>



<h3 class="wp-block-heading" id="other-notable-block-changes">Other notable block changes</h3>



<ul class="wp-block-list">
<li>You can now <a href="https://github.com/WordPress/gutenberg/pull/73790">exclude terms</a> (e.g., categories, tags) via the Query Loop block controls.</li>



<li>On the front-end only, the Paragraph block now has a <code>.wp-block-paragraph</code> class. <a href="https://github.com/WordPress/gutenberg/pull/71207">This change</a> doesn’t affect global styles, which still uses the <code>p</code> selector.</li>



<li>The <a href="https://github.com/WordPress/gutenberg/pull/74722">Verse block utilizes</a> <code>border-box</code> for its <code>box-sizing</code>, which should make it easier to style without additional custom CSS.</li>
</ul>



<h2 class="wp-block-heading" id="playground">Playground</h2>



<p class="wp-block-paragraph">Playground <a href="https://make.wordpress.org/playground/2026/01/16/wordpress-playground-removes-support-for-php-7-2-and-7-3/">removed support for PHP 7.2 and 7.3</a> and bundled several updates for iOS and Safari in the past month. The <a href="https://github.com/WordPress/wordpress-playground/pull/3207">docs were also translated to Bengali</a>.</p>



<p class="wp-block-paragraph"><code>wp-env</code> now <a href="https://make.wordpress.org/playground/2026/02/06/wp-env-now-runs-wordpress-with-playground-runtime/">supports the Playground runtime</a>. By default, it requires Docker to be installed on your machine, which can be an additional hurdle to getting started with WordPress development. Now, with one command, you can run local development with Playground instead:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">npx @wordpress/env start --runtime=playground</code></pre>



<p class="wp-block-paragraph">If you haven’t read it already, be sure to check out <a href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/">Streamlining block theme development with WordPress Playground and Github</a> right here on the Developer Blog.</p>



<h2 class="wp-block-heading" id="notable-user-facing-changes">Notable user-facing changes</h2>



<p class="wp-block-paragraph">A couple of items that are more geared toward the user experience are worth looking at as an extender.</p>



<p class="wp-block-paragraph">View transitions will be <a href="https://core.trac.wordpress.org/ticket/64470">integrated into the WordPress admin</a> in 7.0, enabling smooth transitions between screens. There is an <a href="https://core.trac.wordpress.org/ticket/64471">open ticket</a> to bring this to the front end, but until it is included, you can use the <a href="https://wordpress.org/plugins/view-transitions/">View Transitions plugin</a>.</p>



<p class="wp-block-paragraph">Each heading level (H1-H6) is now <a href="https://github.com/WordPress/gutenberg/pull/73823">registered as a block variation</a> on the Heading block. These do not appear in the inserter, but the change does add icons to the block’s sidebar for transforming it between variations.</p>



<h2 class="wp-block-heading" id="resources">Resources</h2>



<h3 class="wp-block-heading" id="developer-blog">Developer Blog</h3>



<p class="wp-block-paragraph">Three new blog posts landed on the Developer Blog in the past month. If you haven’t read them already, now’s the time:</p>



<ul class="wp-block-list">
<li><a href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/">How to use DataForm to create plugin settings pages</a></li>



<li><a href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/">Streamlining block theme development with WordPress Playground and GitHub</a></li>



<li><a href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/">From Abilities to AI Agents: Introducing the WordPress MCP Adapter</a></li>
</ul>



<p class="wp-block-paragraph"><em>Props to <a class="mention" href="https://profiles.wordpress.org/ndiego/"><span class="mentions-prefix">@</span>ndiego</a>, <a class="mention" href="https://profiles.wordpress.org/fellyph/"><span class="mentions-prefix">@</span>fellyph</a>, <a class="mention" href="https://profiles.wordpress.org/welcher/"><span class="mentions-prefix">@</span>welcher</a>, and <a class="mention" href="https://profiles.wordpress.org/bph/"><span class="mentions-prefix">@</span>bph</a> for contributing to and/or reviewing this article.</em></p>

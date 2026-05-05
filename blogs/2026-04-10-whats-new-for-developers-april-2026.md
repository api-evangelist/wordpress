---
title: "What’s new for developers? (April 2026)"
url: "https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/"
date: "Fri, 10 Apr 2026 16:39:02 +0000"
author: "Jonathan Bossenger"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">One of the more exciting things about working on an open-source project of the size and scope of WordPress is that anything can happen.</p>



<p class="wp-block-paragraph">On <a href="https://make.wordpress.org/core/2026/03/31/extending-the-7-0-cycle/">March 31, 2026, it was announced</a> that the WordPress 7.0 release cycle needed to be extended to get the Real-Time Collaboration (RTC) database architecture right. Then, on April 2nd, a <a href="https://make.wordpress.org/core/2026/04/02/the-path-forward-for-wordpress-7-0/">follow-up post</a> spelled out exactly what that means in practice.</p>



<p class="wp-block-paragraph">It&#8217;s an unusual situation. Returning to beta status after entering the Release Candidate phase is, as the post itself notes, unprecedented. But the reasoning is sound: the current RTC implementation has a performance issue that requires a deeper architectural fix, not a late-cycle patch, before this ships to millions of sites.</p>



<p class="wp-block-paragraph"><strong>Pre-release versions are paused until April 17th</strong>, at which point the release squad and project leadership will have enough context to set a new schedule, to be announced no later than April 22nd.</p>



<p class="wp-block-paragraph">The good news? Everything else in the 7.0 feature set is ready to go. There&#8217;s a lot to cover in this post, so let&#8217;s get into it.</p>



<p class="wp-block-paragraph"><strong>Note:</strong> WordPress 7.0 will drop support for PHP 7.2 and 7.3. The new minimum will be PHP 7.4, with PHP 8.2+ recommended. If you&#8217;re managing sites still running older PHP, that&#8217;s your first action item before the update lands.</p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#highlights">Highlights</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#wordpress-7-0-news-and-updates">WordPress 7.0 news and updates</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#ai-client-and-connectors-api">AI Client and Connectors API </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#client-side-abilities-api">Client-Side Abilities API</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#gutenberg-releases">Gutenberg releases</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#user-facing-changes">User facing changes</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#style-variation-transform-previews">Style variation transform previews</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#playlist-block-waveformplayer">Playlist block WaveformPlayer</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#site-logo-icon-in-the-design-panel">Site Logo &amp; Icon in the Design panel</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#navigation-add-links-directly-from-the-sidebar-list-view">Navigation: add links directly from the sidebar List View</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#plugins-and-tools">Plugins and tools</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#rtc-collaborator-text-selections-now-visible">RTC: Collaborator text selections now visible</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#connectors-extensibility">Connectors extensibility</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#client-side-navigation-block-variant-for-create-block">Client-side navigation block variant for create-block</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#pattern-overrides-for-custom-blocks">Pattern overrides for custom blocks</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#changes-to-the-interactivity-api">Changes to the Interactivity API</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#command-palette-sections-and-recently-used">Command palette: sections and recently used</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#forms-block-hidden-input-field-variation">Forms Block: hidden input field variation</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#themes">Themes</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#button-pseudo-state-styling-in-global-styles">Button pseudo-state styling in Global Styles</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#pseudo-element-support-for-buttons-in-theme-json">Pseudo-element support for buttons in theme.json</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#block-visibility-viewport-based-controls">Block visibility: viewport-based controls</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#navigation-link-style-the-current-menu-item-via-theme-json">Navigation link: style the current menu item via theme.json </a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#tabs-block-inner-block-restructure">Tabs block inner block restructure</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#cover-block-loop-youtube-background-videos">Cover Block: loop YouTube background videos</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#background-gradient-support-for-background-images">Background gradient support for background images</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#playground">Playground</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#wordpress-playground-mcp-server">WordPress Playground MCP server</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#resources">Resources</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#wordpress-7-0-dev-notes-and-field-guide">WordPress 7.0 Dev Notes and Field Guide</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/whats-new-for-developers-april-2026/#developer-blog">Developer Blog</a></li></ol></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="highlights">Highlights</h2>



<h3 class="wp-block-heading" id="wordpress-7-0-news-and-updates">WordPress 7.0 news and updates</h3>



<p class="wp-block-paragraph">The flagship feature of WordPress 7.0 is <a href="https://make.wordpress.org/core/2026/03/10/real-time-collaboration-in-the-block-editor/">Real-Time Collaboration (RTC)</a>. The implementation uses <a href="http://yjs.dev/">Yjs</a> as the underlying CRDT engine, with an HTTP polling sync provider chosen over WebRTC for universal hosting compatibility. The current architecture stores sync data persistently via <code>post_meta</code> on a special <code>wp_sync_storage</code> internal post type, but this approach disables WordPress&#8217;s persistent post query caches whenever a user has the editor open.</p>



<p class="wp-block-paragraph">The fix being worked through now involves a dedicated database table for collaboration data. A new schedule for the remainder of the 7.0 cycle will be published by April 22nd.</p>



<p class="wp-block-paragraph">In the meantime, there&#8217;s still a lot worth knowing:</p>



<ul class="wp-block-list">
<li><strong>Classic meta boxes will disable collaboration mode</strong> for a post. If you&#8217;re still using <code>add_meta_box()</code>, now&#8217;s a good time to consider migrating to <code>register_post_meta()</code> and a <code>PluginSidebar</code> component. The 7.0 cycle is intended to be a window for plugin developers to implement compatibility bridges. If you’re not sure how to migrate your meta boxes to the sidebar, this <a href="https://developer.wordpress.org/news/2023/06/using-block-inspector-sidebar-groups/">tutorial will guide you</a> through the process.</li>



<li><strong>Hosts can customize the sync provider</strong> using the <code>sync.providers</code> filter — useful if you want to offer a WebSocket-based transport on platforms that support it.</li>



<li>For full developer details on RTC, including pitfalls around local state drift and unintended block insertion side effects, read the <a href="https://make.wordpress.org/core/2026/03/10/real-time-collaboration-in-the-block-editor/">RTC Dev Note</a>.</li>
</ul>



<h3 class="wp-block-heading" id="ai-client-and-connectors-api">AI Client and Connectors API </h3>



<p class="wp-block-paragraph">Two major interconnected systems are set to debut in WordPress 7.0:</p>



<p class="wp-block-paragraph"><strong>WP AI Client</strong> is a new core PHP library providing a standardized interface for communicating with AI services. Rather than each plugin integrating directly with OpenAI, Anthropic, Google, or others, the WP AI Client provides a single abstraction layer, so provider switching is a configuration change, not a code rewrite. See the <a href="https://make.wordpress.org/core/2026/03/24/introducing-the-ai-client-in-wordpress-7-0/">Introducing the AI Client in WordPress 7.0</a> dev note for full details.</p>



<p class="wp-block-paragraph"><strong>The Connectors API</strong> establishes credentials storage and provider selection as platform-level infrastructure. As reported in the <a href="https://developer.wordpress.org/news/2026/03/whats-new-for-developers-march-2026/#ai-provider-packages">March edition</a>, the new Connectors screen in the admin will let site owners configure their preferred AI providers using one of the three official provider plugins in the Plugin Directory for <a href="https://wordpress.org/plugins/openai-provider/">OpenAI</a>, <a href="https://wordpress.org/plugins/google-ai-provider/">Google</a>, and <a href="https://wordpress.org/plugins/anthropic-ai-provider/">Anthropic</a>.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="WordPress dashboard showing the new Connectors page" class="wp-image-6029" height="1208" src="https://developer.wordpress.org/news/files/2026/04/Connectors.png" width="2652" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">Since then, community-built providers for <a href="https://wordpress.org/plugins/ai-provider-for-openrouter/">OpenRouter</a>, <a href="https://wordpress.org/plugins/ai-provider-for-ollama/">Ollama</a>, and <a href="https://wordpress.org/plugins/ai-provider-for-mistral/">Mistral</a> have been published, alongside a <a href="https://make.wordpress.org/ai/2026/03/25/call-for-testing-community-ai-connector-plugins/">dedicated call for testing</a>. If you want to build your own provider plugin, the <a href="https://make.wordpress.org/core/2026/03/18/introducing-the-connectors-api-in-wordpress-7-0/">Connectors API Dev Note</a> is a must-read.</p>



<h3 class="wp-block-heading" id="client-side-abilities-api">Client-Side Abilities API</h3>



<p class="wp-block-paragraph">First introduced on the PHP side in WordPress 6.9, the Abilities API now has its JavaScript counterpart landing in 7.0. Two new packages handle it: <code>@wordpress/abilities</code> for pure state management, and <code>@wordpress/core-abilities</code> for the WordPress integration layer, which auto-fetches server-registered abilities via REST. You can register abilities with input/output schemas, permission callbacks, and annotations, laying the groundwork for browser agents and WebMCP integration. Read the <a href="https://make.wordpress.org/core/2026/03/24/client-side-abilities-api-in-wordpress-7-0/">Client-Side Abilities API Dev Note</a> for all the details.</p>



<h3 class="wp-block-heading" id="gutenberg-releases">Gutenberg releases</h3>



<p class="wp-block-paragraph">Three Gutenberg releases landed ahead of the WordPress 7.0 release. You can read the full release posts for each version at the links below, or carry on reading this post for the highlights.</p>



<ul class="wp-block-list">
<li><a href="https://make.wordpress.org/core/2026/03/11/whats-new-in-gutenberg-22-7-11-march/"><strong>Gutenberg 22.7</strong></a></li>



<li><a href="https://make.wordpress.org/core/2026/03/25/whats-new-in-gutenberg-22-8-25-march/"><strong>Gutenberg 22.8</strong></a></li>



<li><a href="https://make.wordpress.org/core/2026/04/09/whats-new-in-gutenberg-22-9-8-april/"><strong>Gutenberg 22.9</strong></a></li>
</ul>



<h2 class="wp-block-heading" id="user-facing-changes">User facing changes</h2>



<h3 class="wp-block-heading" id="style-variation-transform-previews">Style variation transform previews</h3>



<p class="wp-block-paragraph">If your theme offers block style variations, users can now see a <a href="https://make.wordpress.org/core/2026/03/11/whats-new-in-gutenberg-22-7-11-march/#previews-for-style-variation-transforms">live preview of the variation</a> before applying it. Style variations are also now available for patterns in <code>contentOnly</code> mode.</p>



<h3 class="wp-block-heading" id="playlist-block-waveformplayer">Playlist block WaveformPlayer</h3>



<p class="wp-block-paragraph">The Playlist block now has a <a href="https://make.wordpress.org/core/2026/03/11/whats-new-in-gutenberg-22-7-11-march/#playlist-block-now-has-a-visualizer">waveform audio visualization</a> using the <a href="https://github.com/arraypress/waveform-player">@arraypress/waveform-player</a> library. This displays a visual representation of the audio file being listened to, and opens the door to more designs for the block.</p>



<h3 class="wp-block-heading" id="site-logo-icon-in-the-design-panel">Site Logo &amp; Icon in the Design panel</h3>



<p class="wp-block-paragraph">Site logo and icon management is getting a <a href="https://make.wordpress.org/core/2026/03/25/whats-new-in-gutenberg-22-8-25-march/#site-logo-icon-in-the-design-panel">dedicated screen in the Site Editor&#8217;s Design panel</a>, shipping in Gutenberg 22.8. The new screen uses a compact media editor for both fields, making it quicker to set or swap your site&#8217;s logo and favicon without navigating out to admin settings separately. A small but welcome quality-of-life improvement for anyone building or managing block themes.</p>



<h3 class="wp-block-heading" id="navigation-add-links-directly-from-the-sidebar-list-view">Navigation: add links directly from the sidebar List View</h3>



<p class="wp-block-paragraph">You can now <a href="https://github.com/WordPress/gutenberg/pull/75918">add new navigation links directly from the Site Editor&#8217;s sidebar List View</a> for navigation menus, rather than needing to open the block in the editor canvas and interact with the block inspector. It&#8217;s a small quality-of-life change, but one that meaningfully speeds up the process of managing navigation menus in the Site Editor.</p>



<h2 class="wp-block-heading" id="plugins-and-tools">Plugins and tools</h2>



<h3 class="wp-block-heading" id="rtc-collaborator-text-selections-now-visible">RTC: Collaborator text selections now visible</h3>



<p class="wp-block-paragraph">In Gutenberg 22.8, real-time collaboration now shows collaborator <a href="https://make.wordpress.org/core/2026/03/25/whats-new-in-gutenberg-22-8-25-march/#real-time-collaboration-improvements"><strong>text selections</strong></a>, not just cursor positions. When another user selects text, you&#8217;ll see their selection highlighted in their assigned color — consistent with what you&#8217;d expect from collaborative tools like Google Docs. The release also introduced redesigned presence avatars, peer limits, and disconnection debouncing for improved stability.</p>



<h3 class="wp-block-heading" id="connectors-extensibility">Connectors extensibility</h3>



<p class="wp-block-paragraph">Gutenberg 22.8 introduced <a href="https://make.wordpress.org/core/2026/03/25/whats-new-in-gutenberg-22-8-25-march/#connectors-extensibility">extensibility improvements to the Connectors system</a>, allowing third-party provider plugins to integrate more deeply with the Connectors screen and API.</p>



<h3 class="wp-block-heading" id="client-side-navigation-block-variant-for-create-block">Client-side navigation block variant for create-block</h3>



<p class="wp-block-paragraph">The <code>@wordpress/create-block</code> scaffolding tool has a <a href="https://github.com/WordPress/gutenberg/pull/76331">new interactive variant</a> that adds client-side navigation support out of the box. The variant provides a self-contained working example that covers common real-world patterns — query parameter navigation for pagination, search results, and filtered archives — and works immediately after scaffolding, with no additional setup required. If you&#8217;ve ever found the Interactivity API&#8217;s client-side navigation tricky to wire up from scratch, this is a great starting point.</p>



<h3 class="wp-block-heading" id="pattern-overrides-for-custom-blocks">Pattern overrides for custom blocks</h3>



<p class="wp-block-paragraph">Pattern overrides in WordPress 7.0 are being <a href="https://make.wordpress.org/core/2026/03/16/pattern-overrides-in-wp-7-0-support-for-custom-blocks/">extended to support custom blocks</a> — not just core blocks. This means you can create synced patterns that include your own custom blocks while still allowing per-instance content edits. Read the <a href="https://make.wordpress.org/core/2026/03/16/pattern-overrides-in-wp-7-0-support-for-custom-blocks/">Pattern Overrides Dev Note</a> and the <a href="https://make.wordpress.org/core/2026/03/15/pattern-editing-in-wordpress-7-0/">Pattern Editing Dev Note</a> for the full picture.</p>



<h3 class="wp-block-heading" id="changes-to-the-interactivity-api">Changes to the Interactivity API</h3>



<p class="wp-block-paragraph">The Interactivity API has some notable changes heading into 7.0: <code>state.navigation</code> is now <strong>deprecated</strong>. The new <code>watch()</code> function and server-side <code>state.url</code> population enables cleaner patterns for side effects and navigation tracking. If your plugin or theme uses <code>state.navigation</code>, now&#8217;s the time to migrate. See the <a href="https://make.wordpress.org/core/2026/03/04/changes-to-the-interactivity-api-in-wordpress-7-0/">Interactivity API Dev Note</a> for migration guidance.</p>



<h3 class="wp-block-heading" id="command-palette-sections-and-recently-used">Command palette: sections and recently used</h3>



<p class="wp-block-paragraph">The command palette received a <a href="https://github.com/WordPress/gutenberg/pull/75691">structural update in 22.9</a>, introducing <strong>sections</strong> to organize commands into logical groups, along with a <strong>Recently used</strong> section that surfaces your most-used commands at the top. If your plugin registers custom commands via <code>wp.data.dispatch( 'core/commands' )</code>, they&#8217;ll now appear within the appropriate section rather than in a flat list.</p>



<h3 class="wp-block-heading" id="forms-block-hidden-input-field-variation">Forms Block: hidden input field variation</h3>



<p class="wp-block-paragraph">The Forms block gained a <a href="https://github.com/WordPress/gutenberg/pull/74131">hidden input field variation</a> in Gutenberg 22.9. This lets you add hidden fields to block-based forms — useful for tracking parameters, form identifiers, or any metadata you need to pass along on submission without displaying it to the user.</p>



<h2 class="wp-block-heading" id="themes">Themes</h2>



<h3 class="wp-block-heading" id="button-pseudo-state-styling-in-global-styles">Button pseudo-state styling in Global Styles</h3>



<p class="wp-block-paragraph">A new <strong>State</strong> dropdown now appears in Global Styles next to the Button block title. Selecting a state — Hover, Focus, or Active — switches all style controls to edit that specific pseudo-state, with a live preview in the block preview area. No more needing <code>theme.json</code> or custom CSS to style button states. This shipped in <a href="https://github.com/WordPress/gutenberg/pull/75627">Gutenberg 22.8</a>.</p>



<h3 class="wp-block-heading" id="pseudo-element-support-for-buttons-in-theme-json">Pseudo-element support for buttons in theme.json</h3>



<p class="wp-block-paragraph">Theme developers are now able to style <code>:hover</code>, <code>:focus</code>, <code>:focus-visible</code>, and <code>:active</code> states directly on <code>button</code> blocks and their style variations using <code>theme.json</code>. This was previously only possible using custom CSS. The <a href="https://make.wordpress.org/core/2026/03/09/pseudo-element-support-for-blocks-and-their-variations-in-theme-json/">Dev Note</a> contains a detailed example of how this works. This work is part of a broader effort towards a <a href="https://github.com/WordPress/gutenberg/issues/38277">standardized way to modify interactive states</a>.</p>



<h3 class="wp-block-heading" id="block-visibility-viewport-based-controls">Block visibility: viewport-based controls</h3>



<p class="wp-block-paragraph">WordPress 7.0 expands the Block Visibility feature from 6.9. Users will be able to show or hide blocks per device — mobile, tablet, desktop — via the new <code>viewport</code> key inside <code>blockVisibility</code> metadata. Crucially, this is implemented via CSS, <strong>not</strong> DOM removal.</p>



<p class="wp-block-paragraph">If your code assumes <code>blockVisibility</code> is always a boolean, you&#8217;ll need to update it to handle an object as well. No changes are needed if your blocks don&#8217;t interact with the markup server-side. Full details in the <a href="https://make.wordpress.org/core/2026/03/15/block-visibility-in-wordpress-7-0/">Block Visibility Dev Note</a>.</p>



<h3 class="wp-block-heading" id="navigation-link-style-the-current-menu-item-via-theme-json">Navigation link: style the current menu item via theme.json </h3>



<p class="wp-block-paragraph">The Navigation Link block now <a href="https://github.com/WordPress/gutenberg/pull/75736">supports styling the current/active menu item</a> directly via <code>theme.json</code>. Previously, targeting the active state required custom CSS with specificity workarounds. Theme authors can now handle it cleanly in the same place as the rest of their navigation styles.</p>



<h3 class="wp-block-heading" id="tabs-block-inner-block-restructure">Tabs block inner block restructure</h3>



<p class="wp-block-paragraph">The Tabs block has undergone <a href="https://github.com/WordPress/gutenberg/pull/75954">further restructuring of its inner blocks</a> in Gutenberg 22.8, following the significant refactor covered in the <a href="https://developer.wordpress.org/news/2026/02/whats-new-for-developers-february-2026/">February 2026 roundup</a>. The Tabs Menu and inner block structure continue to be refined based on contributor feedback. If you&#8217;re building themes or plugins that style or extend the Tabs block, keep an eye on this <a href="https://github.com/WordPress/gutenberg/issues/73230">tracking issue as it evolves</a>.</p>



<h3 class="wp-block-heading" id="cover-block-loop-youtube-background-videos">Cover Block: loop YouTube background videos</h3>



<p class="wp-block-paragraph">The Cover block now supports <a href="https://github.com/WordPress/gutenberg/pull/76004">a playlist parameter to loop YouTube background videos</a>. Previously, YouTube&#8217;s embed API didn&#8217;t expose a clean way to loop a single video — the block now handles this automatically by passing the correct playlist parameter behind the scenes. No changes needed for existing Cover blocks; the looping behaviour will work automatically for YouTube backgrounds going forward.</p>



<h3 class="wp-block-heading" id="background-gradient-support-for-background-images">Background gradient support for background images</h3>



<p class="wp-block-paragraph">Gutenberg 22.9 adds <a href="https://github.com/WordPress/gutenberg/pull/75859">background gradient support that can combine with background images</a> via block supports. Theme and block developers can now layer a gradient over a background image directly through the block editor&#8217;s design controls — useful for overlays, text readability treatments, and decorative effects without needing custom CSS. If your block registers <code>background</code> support, gradient options will be available alongside existing image controls.</p>



<h2 class="wp-block-heading" id="playground">Playground</h2>



<h3 class="wp-block-heading" id="wordpress-playground-mcp-server">WordPress Playground MCP server</h3>



<p class="wp-block-paragraph">As someone who’s always interested in WordPress AI news, this is one I&#8217;m genuinely excited about. <a href="https://make.wordpress.org/playground/2026/03/17/connect-ai-coding-agents-to-wordpress-playground-with-mcp/">WordPress Playground now has an official MCP server</a> via the new <code>@wp-playground/mcp</code> package. One command wires up Claude Code or Gemini CLI to a browser-based Playground instance over WebSocket, letting your AI agent read and write files, execute PHP, manage sites, and navigate pages — all locally, without touching the WordPress admin.</p>



<pre class="wp-block-code"><code class="">claude mcp add --transport stdio --scope user wordpress-playground -- npx -y @wp-playground/mcp</code></pre>



<p class="wp-block-paragraph">The MCP server exposes tools across four areas:</p>



<ul class="wp-block-list">
<li><strong>Site management:</strong> <code>playground_get_website_url</code>, <code>playground_list_sites</code>, <code>playground_open_site</code>, <code>playground_rename_site</code>, <code>playground_save_site</code></li>



<li><strong>Code execution:</strong> <code>playground_execute_php</code>, <code>playground_request</code></li>



<li><strong>Navigation:</strong> <code>playground_navigate</code>, <code>playground_get_current_url</code>, <code>playground_get_site_info</code></li>



<li><strong>Filesystem:</strong> <code>playground_read_file</code>, <code>playground_write_file</code>, <code>playground_list_files</code>, <code>playground_mkdir</code>, <code>playground_delete_file</code>, and more</li>
</ul>



<p class="wp-block-paragraph">Think plugin testing, live database debugging, and theme scaffolding driven entirely by conversation.</p>



<h2 class="wp-block-heading" id="resources">Resources</h2>



<h3 class="wp-block-heading" id="wordpress-7-0-dev-notes-and-field-guide">WordPress 7.0 Dev Notes and Field Guide</h3>



<p class="wp-block-paragraph">The full Field Guide will be published alongside the rescheduled release. In the meantime, the published dev notes are essential reading if you&#8217;re preparing your plugins or themes. Here&#8217;s the full list so far:</p>



<ul class="wp-block-list">
<li><a href="https://make.wordpress.org/core/2026/03/10/real-time-collaboration-in-the-block-editor/">Real-Time Collaboration in the Block Editor</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/24/introducing-the-ai-client-in-wordpress-7-0/">Introducing the AI Client in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/18/introducing-the-connectors-api-in-wordpress-7-0/">Introducing the Connectors API in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/24/client-side-abilities-api-in-wordpress-7-0/">Client-Side Abilities API in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/03/php-only-block-registration/">PHP-only block registration</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/15/custom-css-for-individual-block-instances-in-wordpress-7-0/">Custom CSS for Individual Block Instances</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/15/new-block-support-text-indent-textindent/">New Block Support: Text Indent (textIndent)</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/15/dimensions-support-enhancements-in-wordpress-7-0/">Dimensions Support Enhancements in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/15/block-visibility-in-wordpress-7-0/">Block Visibility in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/16/pattern-overrides-in-wp-7-0-support-for-custom-blocks/">Pattern Overrides in WordPress 7.0: Support for Custom Blocks</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/15/pattern-editing-in-wordpress-7-0/">Pattern Editing in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/09/pseudo-element-support-for-blocks-and-their-variations-in-theme-json/">Pseudo-element support for blocks and their variations in theme.json</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/04/changes-to-the-interactivity-api-in-wordpress-7-0/">Changes to the Interactivity API in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/04/dataviews-dataform-et-al-in-wordpress-7-0/">DataViews, DataForm, et al. in WordPress 7.0</a></li>



<li>Customizable <a href="https://make.wordpress.org/core/2026/03/04/customisable-navigation-overlays-in-wordpress-7-0/">Navigation Overlays in WordPress 7.0</a></li>



<li><a href="https://make.wordpress.org/core/2026/03/04/breadcrumb-block-filters/">Breadcrumb block filters</a></li>
</ul>



<p class="wp-block-paragraph">Keep an eye on <a href="https://make.wordpress.org/core">make.wordpress.org/core</a> for additional dev notes and the updated release schedule as they&#8217;re published.</p>



<h3 class="wp-block-heading" id="developer-blog">Developer Blog</h3>



<ul class="wp-block-list">
<li>If you&#8217;re currently using <code>@wordpress/scripts</code>, this one&#8217;s for you. JuanMa Garrido published <a href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/">a detailed introduction to <code>@wordpress/build</code></a> on the Developer Blog. The new tool replaces the webpack and Babel pipeline with a significantly faster esbuild-based engine and automatically generates PHP registration files from <code>package.json</code>. The migration path for existing <code>@wordpress/scripts</code> users is designed to be low-friction. If you&#8217;re planning to update your plugin&#8217;s build tooling, that post is essential reading.</li>
</ul>



<p class="wp-block-paragraph">Never want to miss an article again? <a href="https://developer.wordpress.org/news/subscribe/">Subscribe to the WordPress Developer Blog</a>.</p>



<p class="has-text-align-right wp-block-paragraph"><em>Props to&nbsp;<a class="mention" href="https://profiles.wordpress.org/greenshady/"><span class="mentions-prefix">@</span>greenshady</a> and <a class="mention" href="https://profiles.wordpress.org/areziaal/"><span class="mentions-prefix">@</span>areziaal</a> for reviewing this article.</em></p>



<p class="wp-block-paragraph"></p>

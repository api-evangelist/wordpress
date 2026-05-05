---
title: "@wordpress/build, the next generation of WordPress plugin build tooling"
url: "https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/"
date: "Thu, 02 Apr 2026 17:26:38 +0000"
author: "JuanMa Garrido"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">WordPress build tooling is about to change. But not in a disruptive way. Most developers who use <code>@wordpress/scripts</code> today will not need to change anything when the transition happens. But the underlying engine, the philosophy, and the developer experience are all shifting, and the window to influence that direction is open right now.</p>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/tree/trunk/packages/wp-build"><code>@wordpress/build</code></a> is the tool driving that shift. It replaces the webpack and Babel pipeline with a significantly faster build engine, auto-generates PHP registration files from <code>package.json</code> conventions, and handles scripts, <a href="https://developer.wordpress.org/reference/functions/wp_register_script_module/">script modules</a>, and styles in one pass. It works through convention-based folder discovery: a <code>packages/</code> directory for JavaScript packages and a <code>routes/</code> directory for admin page routes, each auto-discovered with no configuration. Gutenberg already uses it to build all of its 100+ packages. The long-term plan is for it to become the engine underneath <code>@wordpress/scripts</code>, so every plugin developer benefits from the same tooling, without changing their workflow.</p>



<p class="wp-block-paragraph"><code>@wordpress/build</code> is not ready for every use case yet. In particular, a plugin registering blocks, a common entry point for WordPress plugin developers, still has gaps that require manual workarounds. But as Riad Benguella noted when <a href="https://github.com/WordPress/gutenberg/issues/72032">introducing the vision</a>:</p>



<blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow">
<p class="wp-block-paragraph">&#8220;I can&#8217;t find edge cases by only working on Gutenberg.&#8221;</p>
</blockquote>



<p class="wp-block-paragraph">This article explains what <code>@wordpress/build</code> does, how it works inside Gutenberg today, what it means for plugin developers, and, crucially, where the project needs your feedback while the API is still being shaped.</p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#the-vision">The vision</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#a-faster-and-simpler-build-process">A faster and simpler build process</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#how-it-works">How it works</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#configuration">Configuration</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#auto-generated-php-registration">Auto-generated PHP registration</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#the-namespace-model">The namespace model</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#who-should-engage-with-it-today">Who should engage with it today</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#help-shape-the-tool">Help shape the tool</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#block-plugin-structure-and-registration">Block plugin structure and registration</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#the-setup-experience-outside-a-monorepo">The setup experience outside a monorepo</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#the-externals-and-namespace-model">The externals and namespace model</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#the-convergence-roadmap">The convergence roadmap</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/04/wordpress-build-the-next-generation-of-wordpress-plugin-build-tooling/#resources">Resources</a></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="the-vision">The vision</h2>



<p class="wp-block-paragraph"><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/"><code>@wordpress/scripts</code></a> has served plugin developers well since the block editor launched. It preconfigures webpack, handles dependency extraction via <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dependency-extraction-webpack-plugin/"><code>@wordpress/dependency-extraction-webpack-plugin</code></a>, and generates <code>.asset.php</code> files. But it accumulated complexity over the years: custom Babel plugins, flexible (and therefore complex) webpack configurations. And it has a telling limitation: Gutenberg itself never used it to build its own packages. Core relied on separate custom tooling.</p>



<p class="wp-block-paragraph">In October 2025, Riad Benguella opened <a href="https://github.com/WordPress/gutenberg/issues/72032">issue #72032</a> &#8220;WordPress Scripts: A vision for a v2 version&#8221;:</p>



<blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow">
<p class="wp-block-paragraph">What if instead of flexibility, we absorb complexity into the tool to make plugin development as easy as it should have been? You want a new block, just add a &#8220;blocks&#8221; folder with a list of blocks. You want a new page in wp-admin, just add a folder with an index file for that page. But the build command is always the same — <code>wp-scripts build</code>, no arguments, nothing.</p>
</blockquote>



<p class="wp-block-paragraph">The proposal: replace configuration with convention. Place your code in known folders,  <code>packages/</code> for JavaScript packages or <code>routes/</code> for admin pages,  declare what each package is through <code>package.json</code> fields, and run a single <code>wp-build</code> command that discovers everything and figures out the rest. No webpack config, no entry point lists, no Babel pipeline. And critically: PHP registration generated automatically, not written by hand.</p>



<p class="wp-block-paragraph"><a href="https://github.com/WordPress/gutenberg/pull/72743">PR #72743</a> introduced <code>@wordpress/build</code> as a standalone package in October 2025, and it became Gutenberg&#8217;s internal build tool. The next step is making it work for everyone.</p>



<h2 class="wp-block-heading" id="a-faster-and-simpler-build-process">A faster and simpler build process</h2>



<p class="wp-block-paragraph">The JavaScript ecosystem has moved well beyond the webpack and Babel era. Native-speed bundlers (tools written in Go, Rust, and other compiled languages) can parse, transpile, and bundle in a fraction of the time, often by handling everything in a single pass rather than through a multi-tool pipeline.</p>



<p class="wp-block-paragraph"><code>@wordpress/build</code> takes advantage of this. Its current internal engine is <a href="https://esbuild.github.io/">esbuild</a>, a Go-based bundler that replaces the separate webpack bundling and Babel transpilation steps. For a large project like Gutenberg (100+ packages), full builds that took minutes now take seconds. In watch mode, <code>wp-build --watch</code> uses incremental rebuilds, and only the changed package and its dependents are recompiled, making the feedback loop near-instant.</p>



<p class="wp-block-paragraph">The use of esbuild as a bundler is an internal implementation detail: not exposed in the API, and subject to change without any impact on how you use the tool.</p>



<p class="wp-block-paragraph">Speed is part of the picture, but it does not explain why <code>@wordpress/build</code> requires almost no configuration. That comes from the tool&#8217;s opinionated nature. <code>@wordpress/scripts</code> accumulated complexity not because of webpack, but because of the choice to keep it as a thin, flexible wrapper — one that you can customize for your needs. <code>@wordpress/build</code> makes the opposite bet: absorb the complexity into the tool and provide a set of conventions for common cases.</p>



<h2 class="wp-block-heading" id="how-it-works">How it works</h2>



<p class="wp-block-paragraph"><code>@wordpress/build</code> uses a convention-based discovery model. Place your code in known top-level folders and the tool finds it automatically:</p>



<ul class="wp-block-list">
<li><strong><code>packages/</code></strong> — JavaScript packages. Each subdirectory is a package with its own <code>package.json</code>. The tool scans <code>packages/*/package.json</code> to discover what to build.</li>



<li><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#routes-experimental"><strong><code>routes/</code></strong></a> <em>(experimental)</em> — Admin page routes. Each subdirectory defines a route with a <code>package.json</code> mapping it to a page and URL path. Components and lifecycle hooks are bundled automatically. Requires pages to be declared in <code>wpPlugin.pages</code> in the root <code>package.json</code>.</li>
</ul>



<p class="wp-block-paragraph">A <code>blocks/</code> folder following the same pattern is <a href="https://github.com/WordPress/gutenberg/issues/74542">proposed in issue #74542</a> (see <a href="#block-plugin-structure-and-registration">Block plugin structure and registration</a> below).</p>



<p class="wp-block-paragraph">No separate build config file is needed. Discovery is driven by folder structure; a small set of <code>package.json</code> fields handles the rest.</p>



<div class="wp-block-wporg-notice is-info-notice"><div class="wp-block-wporg-notice__icon"></div><div class="wp-block-wporg-notice__content"><p>These folder names are fixed conventions — <code>packages/</code>, <code>routes/</code>, <code>blocks/</code> cannot be renamed or pointed elsewhere via config or CLI flags. If your project already uses these directory names for other purposes, you&#8217;ll need to restructure before adopting the tool. This is a known constraint and <a href="https://github.com/WordPress/gutenberg/issues">worth raising</a> if it affects your workflow.</p></div></div>



<h3 class="wp-block-heading" id="configuration">Configuration</h3>



<p class="wp-block-paragraph">Custom settings that can&#8217;t be inferred from the folder structure live at two levels:</p>



<ul class="wp-block-list">
<li><strong>Root <code>package.json</code></strong> (plugin level) — plugin-wide settings: the namespace, the global variable name, the handle prefix, and any external namespaces from other plugins. This is the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#root-configuration"><code>wpPlugin</code> block</a>.</li>



<li><strong>Unit <code>package.json</code></strong> (one per discovered unit, inside <code>packages/</code>, <code>routes/</code> <em>(experimental)</em>, or similar) — per-unit settings: whether it registers as a script (<a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpscript"><code>wpScript</code></a>) or a script module (<a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpscriptmoduleexports"><code>wpScriptModuleExports</code></a>). Packages that need Web Workers use <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpworkers"><code>wpWorkers</code></a> to define self-contained worker bundles, which are compiled with all dependencies inlined and loadable via Blob URLs.</li>
</ul>



<p class="wp-block-paragraph">Here is <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#example-wordpress-core-gutenberg">Gutenberg&#8217;s root configuration</a>:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "wpPlugin": {
    "name": "gutenberg",
    "scriptGlobal": "wp",
    "packageNamespace": "wordpress",
    "handlePrefix": "wp"
  }
}</code></pre>



<p class="wp-block-paragraph">And a package-level configuration for a simple utility package:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "name": "@wordpress/api-fetch",
  "wpScript": true,
  "wpScriptModuleExports": {
    ".": "./build-module/index.mjs"
  }
}</code></pre>



<p class="wp-block-paragraph">Two fields replace what would otherwise be webpack config, Babel plugins, and hand-written PHP:</p>



<ul class="wp-block-list">
<li><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpscript"><strong><code>wpScript: true</code></strong></a> — bundle as an <a href="https://developer.mozilla.org/en-US/docs/Glossary/IIFE">IIFE</a> (Immediately Invoked Function Expression), register as a WordPress script at <code>window.wp.apiFetch</code> with handle <code>wp-api-fetch</code></li>



<li><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpscriptmoduleexports"><strong><code>wpScriptModuleExports</code></strong></a> — expose entry points as ESM <a href="https://developer.wordpress.org/reference/functions/wp_register_script_module/">script modules</a></li>
</ul>



<h3 class="wp-block-heading" id="auto-generated-php-registration">Auto-generated PHP registration</h3>



<p class="wp-block-paragraph"><code>@wordpress/build</code> generates the WordPress registration layer for scripts, modules, and styles. A single line in your plugin file:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">require_once plugin_dir_path( __FILE__ ) . 'build/build.php';</code></pre>



<p class="wp-block-paragraph">This loads <code>scripts.php</code>, <code>modules.php</code>, and <code>styles.php</code> ,generated files that hook into <code>wp_default_scripts</code> and <code>wp_default_styles</code> to register every script, module, and style your packages produce. The <code>.asset.php</code> files track dependencies automatically from your imports, including the distinction between <code>static</code> and <code>dynamic</code> module imports that WordPress uses to optimize the import map.</p>



<h2 class="wp-block-heading" id="the-namespace-model">The namespace model</h2>



<p class="wp-block-paragraph">If you have used <code>@wordpress/scripts</code>, you are familiar with how <code>@wordpress/dependency-extraction-webpack-plugin</code> externalizes <code>@wordpress/*</code> imports: <code>import { __ } from '@wordpress/i18n'</code> becomes a reference to <code>window.wp.i18n</code> at runtime rather than bundling the package (see <a href="https://developer.wordpress.org/news/2023/04/how-webpack-and-wordpress-packages-interact/">How webpack and WordPress packages interact</a>). <code>@wordpress/build</code> bakes this in and extends it.</p>



<p class="wp-block-paragraph">Your <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpplugin-packagenamespace"><code>wpPlugin</code> namespace configuration</a> determines how your own packages are externalized. A package named <code>@acme/editor</code> with <code>wpScript: true</code> is bundled as an IIFE at <code>window.acme.editor</code> with handle <code>acme-editor</code>. When another package in your plugin imports from <code>@acme/editor</code>, that import is automatically externalized: the bundle references the global instead of duplicating the module, and <code>acme-editor</code> is declared in the <code>.asset.php</code> dependencies.</p>



<p class="wp-block-paragraph">The same model works across plugins. Declare another plugin&#8217;s namespace as external:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "wpPlugin": {
    "externalNamespaces": {
      "woo": { "global": "woo", "handlePrefix": "woocommerce" }
    }
  }
}</code></pre>



<p class="wp-block-paragraph">Now <code>import { Cart } from '@woo/cart'</code> resolves to <code>window.woo.cart</code> at runtime, and <code>woocommerce-cart</code> appears automatically in your <code>.asset.php</code> dependencies so WordPress loads WooCommerce&#8217;s script before yours without any manual dependency declaration.</p>



<h2 class="wp-block-heading" id="who-should-engage-with-it-today">Who should engage with it today</h2>



<p class="wp-block-paragraph"><strong>Gutenberg contributors.</strong> When you run <code>npm start</code> in the <a href="https://developer.wordpress.org/block-editor/contributors/code/getting-started-with-code-contribution/">Gutenberg repository</a>, <code>@wordpress/build</code> is what executes. Understanding the <code>wpPlugin</code> config, the <code>wpCopyFiles</code> transforms, and the externals resolution helps you debug build issues and understand how Gutenberg ships code to WordPress core.</p>



<p class="wp-block-paragraph"><strong>Developers building plugins with multiple scripts or packages.</strong> <code>@wordpress/build</code> is not limited to monorepos. Each JavaScript entry point can be its own package: just add <code>"private": true</code> to its <code>package.json</code> and place it under <code>packages/</code>. This means the tool is viable for most plugin architectures, not just those structured as multi-package npm workspaces. If your plugin has multiple scripts, modules, or admin pages that currently require separate webpack entry points or hand-written PHP registration, the convention-based model is worth evaluating.</p>



<p class="wp-block-paragraph"><strong>Developers who want to help shape the tool.</strong> The API is malleable right now. If you care about how WordPress build tooling works, this is the moment to engage. Try the tool, hit the rough edges, file what you find.</p>



<p class="wp-block-paragraph"><strong>Everyone else: stay on <code>@wordpress/scripts</code>.</strong> For single-block plugins, <code>@wordpress/create-block</code> gives you a working block in one command. For plugins maintaining a stable webpack setup, the convergence with <code>@wordpress/scripts</code> will bring the benefits without requiring migration. For most developers, waiting for that convergence is the lower-friction path, though if your plugin&#8217;s needs align with the current conventions, migrating earlier is a legitimate option.</p>



<h2 class="wp-block-heading" id="help-shape-the-tool">Help shape the tool</h2>



<p class="wp-block-paragraph">These are the areas where the design is unresolved and your experience can directly shape the outcome.</p>



<h3 class="wp-block-heading" id="block-plugin-structure-and-registration">Block plugin structure and registration</h3>



<p class="wp-block-paragraph"><code>@wordpress/build</code> already supports an experimental <code>routes/</code> folder at the project root. Place it alongside <code>packages/</code>, declare your pages in <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpplugin-pages-experimental"><code>wpPlugin.pages</code></a> in the root <code>package.json</code>, and each route maps itself to a declared page via a <code>route.page</code> field in its own <code>package.json</code>. <a href="https://github.com/WordPress/gutenberg/issues/74542">Issue #74542</a> proposes the same auto-discovery pattern for blocks:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">my-plugin/
├── packages/        # JS packages (already supported)
├── routes/          # Admin page routes (experimental, already supported)
└── blocks/          # <span class="wp-exclude-emoji">←</span> proposed: blocks auto-discovered here
    ├── notice-box/
    │   ├── block.json
    │   ├── index.js
    │   ├── edit.js
    │   ├── save.js
    │   ├── render.php
    │   └── style.scss
    └── progress-bar/
        └── ...</code></pre>



<p class="wp-block-paragraph">Drop a folder in <code>blocks/</code>, run <code>wp-build</code>, and get a generated <code>build/blocks.php</code> that handles all registration: no <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build/#wpcopyfiles"><code>wpCopyFiles</code></a> configuration, no manual PHP loader, no style registration boilerplate. The proposal also targets making this the default for <code>@wordpress/create-block</code>, replacing <code>@wordpress/scripts</code> as the scaffolding target.</p>



<p class="wp-block-paragraph">The question for block plugin developers: does this structure work for how you build plugins today? Is a <code>blocks/</code> folder at the root the right convention, or do you need something different? The issue has eight comments but needs broader input from developers outside the Gutenberg team. If block development is your primary use case, <a href="https://github.com/WordPress/gutenberg/issues/74542">#74542</a> is the most valuable place to contribute.</p>



<p class="wp-block-paragraph">Also related, the issue <a href="https://github.com/WordPress/gutenberg/issues/75832">#75832</a> covers whether the manifest should register blocks with <code>WP_Block_Metadata_Registry</code> (the <a href="https://developer.wordpress.org/reference/functions/wp_register_block_types_from_metadata_collection/"><code>wp_register_block_types_from_metadata_collection()</code></a> approach introduced in WordPress 6.8, see the <a href="https://make.wordpress.org/core/2025/03/13/more-efficient-block-type-registration-in-6-8/">WordPress 6.8 dev note</a>).</p>



<h3 class="wp-block-heading" id="the-setup-experience-outside-a-monorepo">The setup experience outside a monorepo</h3>



<p class="wp-block-paragraph">Setting up <code>@wordpress/build</code> in a standalone plugin currently requires: npm workspaces (for cross-package import resolution), <code>@wordpress/*</code> packages physically installed (the externals plugin reads their metadata), and <code>@babel/core</code> as a hidden dependency when <code>@wordpress/components</code> is in your tree. None of this is documented.</p>



<p class="wp-block-paragraph">Try the tool. Every friction point you report helps bridge the gap between &#8220;works for Gutenberg&#8221; and &#8220;works for everyone.&#8221;</p>



<h3 class="wp-block-heading" id="the-externals-and-namespace-model">The externals and namespace model</h3>



<p class="wp-block-paragraph">The build reads installed <code>@wordpress/*</code> package metadata to decide how to externalize each import: as a classic script global or a script module. This model also enables cross-plugin interoperability via <code>externalNamespaces</code>. Does it cover your plugin architecture? Are there dependency patterns it does not support?</p>



<p class="wp-block-paragraph">Issue <a href="https://github.com/WordPress/gutenberg/issues/75196">#75196 — Build: Update tools to recognize module dependencies of scripts</a> was opened around this topic.</p>



<div class="wp-block-wporg-notice is-tip-notice"><div class="wp-block-wporg-notice__icon"></div><div class="wp-block-wporg-notice__content"><p>Any friction you hit or suggestion of improvement can be reported in the <a href="https://github.com/WordPress/gutenberg/issues">Gutenberg repository</a>.</p></div></div>



<h2 class="wp-block-heading" id="the-convergence-roadmap">The convergence roadmap</h2>



<p class="wp-block-paragraph"><code>@wordpress/build</code> is designed to become the engine underneath <code>@wordpress/script</code>, not to replace it externally, but to power it from within:</p>



<ol class="wp-block-list">
<li><strong>Today</strong>: standalone package, used internally by Gutenberg. Third-party adoption requires working around some of the gaps described above.</li>



<li><strong>Next</strong>: <code>@wordpress/scripts</code> adopts <code>@wordpress/build</code> as its build engine. <code>wp-scripts build</code> continues to work; transpilation and bundling shift to use wp-build internally.</li>



<li><strong>Eventually</strong>: webpack and Babel are deprecated from <code>@wordpress/scripts</code>. Developers using the default setup see faster builds and auto-generated PHP registration. Developers with custom webpack configs get a migration guide.</li>
</ol>



<p class="wp-block-paragraph">The features in <code>@wordpress/build</code> today, PHP transforms, script module support with static/dynamic tracking and RTL generation, will reach every <code>wp-scripts build</code> user through this path. How smooth that transition is depends on how much the rough edges get filed before the API stabilises.</p>



<p class="wp-block-paragraph">Track the vision in <a href="https://github.com/WordPress/gutenberg/issues/72032">issue #72032</a>. If you work with WordPress build tooling, now is the time to engage.</p>



<h2 class="wp-block-heading" id="resources">Resources</h2>



<ul class="wp-block-list">
<li><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-wp-build"><code>@wordpress/build</code> documentation</a></li>



<li><a href="https://github.com/WordPress/gutenberg/tree/trunk/packages/wp-build"><code>@wordpress/build</code> package source and README</a></li>



<li><a href="https://github.com/WordPress/gutenberg/issues/72032">Issue #72032 — &#8220;WordPress Scripts: A vision for a v2 version&#8221;</a></li>



<li><a href="https://github.com/WordPress/gutenberg/pull/72743">PR #72743 — initial implementation</a></li>



<li><a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/"><code>@wordpress/scripts</code> documentation</a></li>



<li><a href="https://developer.wordpress.org/block-editor/contributors/code/getting-started-with-code-contribution/">Getting started with Gutenberg code contributions</a></li>
</ul>



<p class="wp-block-paragraph"><em>Props to <a class="mention" href="https://profiles.wordpress.org/youknowriad/"><span class="mentions-prefix">@</span>youknowriad</a>, <a class="mention" href="https://profiles.wordpress.org/greenshady/"><span class="mentions-prefix">@</span>greenshady</a> and <a class="mention" href="https://profiles.wordpress.org/welcher/"><span class="mentions-prefix">@</span>welcher</a> for reviewing this post</em></p>



<p class="wp-block-paragraph"></p>

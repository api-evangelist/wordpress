---
title: "Streamlining block theme development with WordPress Playground and GitHub"
url: "https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/"
date: "Fri, 23 Jan 2026 09:17:32 +0000"
author: "Birgit Pauli-Haack"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">Block themes and the Site Editor have transformed the WordPress design landscape, making professional theme development accessible to designers who prefer visual interfaces over code. This shift opens the ecosystem to a new group of creators who previously relied on external design tools. However, a significant hurdle remains: how can changes made within the Site Editor’s database be extracted into a theme&#8217;s file system and integrated into a version-controlled workflow?</p>



<p class="wp-block-paragraph">This article details a &#8220;no-code&#8221; development workflow that uses a powerful combination of tools—<strong>WordPress Playground</strong>, the <strong>Create Block Theme (CBT)</strong> plugin, and <strong>GitHub</strong>—to bridge the gap between browser-based design and professional version control.</p>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#the-core-challenge-of-site-editor-changes">The core challenge of Site Editor changes</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#a-closer-look-at-the-tools">A closer look at the tools</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#setting-up-the-workbench">Setting up the workbench</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#importing-the-theme-from-github">Importing the theme from GitHub</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#designing-and-syncing-changes">Designing and syncing changes</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#submitting-a-pull-request-via-playground">Submitting a Pull Request via Playground</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/streamlining-block-theme-development-with-wordpress-playground-and-github/#use-cases-for-this-workflow">Use cases for this workflow</a></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="the-core-challenge-of-site-editor-changes">The core challenge of Site Editor changes</h2>



<p class="wp-block-paragraph">In the WordPress block editor environment, design, and styling exist at four levels:</p>



<ul class="wp-block-list">
<li><strong>Default </strong>mostly the styling and layouts of WordPress Core.</li>



<li><strong>Block-level</strong> styling can be altered with plugins and overwrites the Default styling.</li>



<li><strong>Theme-level </strong>styling is the whole suite of design tools, controlled by the active Theme. It overwrites Default and block-level styles and layouts for instance (e.g. template and template parts).</li>



<li><strong>User-level</strong> styling uses the Design tools within the Site Editor to modify styles and layouts. These changes are stored in the database and overwrite the theme-level styling.</li>
</ul>



<figure class="wp-block-image size-full is-resized wp-lightbox-container"><img alt="Hierarchy for theme changes. " class="wp-image-5700" height="392" src="https://developer.wordpress.org/news/files/2025/12/Screenshot-2025-12-18-at-18.20.34.png" style="width: 667px; height: auto;" width="667" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">As mentioned, when a designer modifies a template in the Site Editor, those changes are stored in the database as &#8220;user-level&#8221; customizations. Without a way to sync these changes back to the theme’s files (the &#8220;theme level&#8221;), they cannot be easily reused on other sites, version-controlled, or protected from being overwritten during updates.</p>



<h2 class="wp-block-heading" id="a-closer-look-at-the-tools">A closer look at the tools</h2>



<p class="wp-block-paragraph">To understand how this workflow bridges the gap between visual design and version-controlled development, it is helpful to look at the specific roles of each tool in the stack.</p>



<p class="wp-block-paragraph"><strong><a href="https://wordpress.org/playground/">WordPress Playground</a></strong> runs a full WordPress instance entirely within your web browser using WebAssembly (WASM). It requires no installation, no server setup, and no traditional database. It acts as a &#8220;disposable&#8221; workbench where you can spin up a specific environment, test designs, and close the tab when finished.</p>



<p class="wp-block-paragraph">The <a href="https://wordpress.org/plugins/create-block-theme/"><strong>Create Block Theme (CBT)</strong> </a>plugin provides the critical <strong>Save Changes to Theme </strong>feature. It takes modifications stored in the WordPress database and writes them directly into the theme&#8217;s virtual file system within Playground, updating <code>theme.json</code> and HTML templates automatically.</p>



<p class="wp-block-paragraph"><strong><a href="https://github.com/">GitHub</a></strong> provides the version control (Git) that allows you to track changes and collaborate. In this workflow, GitHub is the &#8220;Permanent Storage.&#8221; By connecting Playground to a GitHub repository, you move from &#8220;one-off&#8221; site building into a professional lifecycle where changes are submitted via <a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests">Pull Requests</a> (PRs).</p>



<h2 class="wp-block-heading" id="setting-up-the-workbench">Setting up the workbench</h2>



<p class="wp-block-paragraph">The workflow begins by launching a pre-configured Playground instance. You can launch a workbench with the necessary tools already installed by appending plugin slugs to the Playground URL: <a href="https://playground.wordpress.net/?plugin=gutenberg&amp;plugin=create-block-theme&amp;url=/wp-admin/site-editor.php">https://playground.wordpress.net/?plugin=gutenberg&amp;plugin=create-block-theme</a></p>



<div class="wp-block-wporg-notice is-tip-notice"><div class="wp-block-wporg-notice__icon"></div><div class="wp-block-wporg-notice__content"><p><strong>Note:</strong> Once the instance is loaded, set the storage type to <strong>&#8220;Browser&#8221;</strong> within the Playground settings (the site manager icon <img alt="" class="wp-image-5723" height="24" src="https://developer.wordpress.org/news/files/2025/12/Screenshot-2025-12-19-at-13.26.21.png" style="width: 18px;" width="26" />) to ensure changes persist if you accidentally refresh the page.</p></div></div>



<figure class="wp-block-image size-large wp-lightbox-container"><img alt="Screen to save the Playground instance " class="wp-image-5720" height="487" src="https://developer.wordpress.org/news/files/2025/12/Screenshot-2025-12-19-at-13.06.19-1024x487.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="importing-the-theme-from-github">Importing the theme from GitHub</h3>



<p class="wp-block-paragraph">To work on an existing project, the theme must be imported from its GitHub repository:</p>



<ol class="wp-block-list" start="1">
<li>Open the Playground menu and select <strong>Import from GitHub</strong>.</li>



<li>Authenticate the connection to GitHub.</li>



<li>Provide the repository URL and specify that the import is a <strong>Theme</strong>.</li>



<li>Identify the correct directory (usually the root <code>/</code>).</li>
</ol>



<p class="wp-block-paragraph">Playground will download the theme files and activate the theme within the browser instance and reload the site. </p>



<figure class="wp-block-gallery alignfull has-nested-images columns-3 wp-block-gallery-1 is-layout-flex wp-block-gallery-is-layout-flex">
<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Step 1: connect to GitHub" class="wp-image-5800" height="305" src="https://developer.wordpress.org/news/files/2026/01/Screenshot-2026-01-20-at-19.00.11.png" width="679" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Step 2: Identify the GitHub repository" class="wp-image-5799" height="250" src="https://developer.wordpress.org/news/files/2026/01/Screenshot-2026-01-20-at-19.01.39.png" title="Screenshot 2025-09-18 at 17.00.28.png" width="664" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Step 3: Tell Playground about the nature of the GitHub repository" class="wp-image-5798" height="403" src="https://developer.wordpress.org/news/files/2026/01/Screenshot-2026-01-20-at-19.02.01.png" title="Screenshot 2025-09-18 at 17.26.34.png" width="664" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>
<figcaption class="blocks-gallery-caption wp-element-caption">Three workflow screens to import a Theme from GitHub</figcaption></figure>



<h2 class="wp-block-heading" id="designing-and-syncing-changes">Designing and syncing changes</h2>



<p class="wp-block-paragraph">With the theme active, modifications are made directly within the <strong>Site Editor</strong>. After saving changes in the Site Editor, they must be written to the theme files:</p>



<ol class="wp-block-list" start="1">
<li>Open the <strong>CBT sidebar</strong> within the editor (click the wrench icon in the top toolbar).</li>



<li>Select <strong>Save Changes to Theme</strong>.</li>



<li>Optionally select <strong>Localize Images</strong> to move uploaded media from the database to the theme&#8217;s <code>/assets</code> folder. The folder is customizable via a WordPress filter. </li>
</ol>



<p class="wp-block-paragraph">This step moves the modifications from the WordPress database into the virtual file system of the Playground instance, preparing them for a GitHub commit.</p>



<p class="wp-block-paragraph">&nbsp;&nbsp;&nbsp;</p>



<figure class="wp-block-gallery has-nested-images columns-default wp-block-gallery-2 is-layout-flex wp-block-gallery-is-layout-flex">
<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Create Block Theme plugin: Save the changes Part 1" class="wp-image-5704" height="484" src="https://developer.wordpress.org/news/files/2025/12/image-7.png" title="Screenshot 2025-09-18 at 18.12.51.png" width="255" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Create Block Theme plugin: Save the changes Part 2" class="wp-image-5705" height="432" src="https://developer.wordpress.org/news/files/2025/12/image-8.png" title="Screenshot 2025-09-18 at 18.12.57.png" width="235" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>
</figure>



<h2 class="wp-block-heading" id="submitting-a-pull-request-via-playground">Submitting a Pull Request via Playground</h2>



<p class="wp-block-paragraph">Once the design is synced to the files, the changes can be submitted back to GitHub without leaving the browser:</p>



<ol class="wp-block-list" start="1">
<li>Open the Playground menu and select <strong>Export to GitHub</strong>.</li>



<li>Playground automatically populates the repository information.</li>



<li>Enter a descriptive <strong>commit message</strong>.</li>



<li>Click <strong>Create Pull Request</strong>.</li>
</ol>



<figure class="wp-block-gallery alignwide has-nested-images columns-default wp-block-gallery-3 is-layout-flex wp-block-gallery-is-layout-flex">
<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Step 1: Export to GitHub " class="wp-image-5708" height="268" src="https://developer.wordpress.org/news/files/2025/12/image-11.png" title="Screenshot 2025-09-18 at 12.14.43.png" width="253" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Step 2 Export to GitHub with commit message" class="wp-image-5709" height="656" src="https://developer.wordpress.org/news/files/2025/12/image-12.png" title="Screenshot 2025-09-18 at 18.54.39.png" width="545" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Step 3: Success message + link to PR on GitHub. " class="wp-image-5712" height="214" src="https://developer.wordpress.org/news/files/2025/12/image-13.png" title="Screenshot 2025-09-18 at 18.23.04.png" width="542" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>
<figcaption class="blocks-gallery-caption wp-element-caption">The three screens to create a Pull Request in GitHub </figcaption></figure>



<p class="wp-block-paragraph">In the last step, you will find a link to the created GitHub PR, where you can continue submitting it as a code commit. </p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Screenshot of a Pull Request, created by Playground. " class="wp-image-5713" height="567" src="https://developer.wordpress.org/news/files/2025/12/image-14.png" title="Screenshot 2025-09-18 at 18.59.10.png" width="791" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">The developer can then visit GitHub to review the changes and merge the Pull Request into the main project. </p>



<h2 class="wp-block-heading" id="use-cases-for-this-workflow">Use cases for this workflow</h2>



<p class="wp-block-paragraph"><strong>The Designer-to-Developer handoff:</strong> A designer works visually in the Site Editor, saves changes via CBT, and submits a PR. The developer reviews the code in GitHub, ensuring it meets standards before merging. This eliminates the &#8220;translation&#8221; phase from design tools to code.</p>



<p class="wp-block-paragraph"><strong>Rapid prototyping and client previews:</strong> Spin up a Playground instance, make requested layout changes visually, and share the project&#8217;s Playground URL with the client for instant feedback—without touching a staging server.</p>



<p class="wp-block-paragraph"><strong>Open-source theme contributions:</strong> This democratizes contributions. Anyone can click a link to open a theme in Playground, fix a styling bug visually, and submit a PR without ever opening a terminal or a code editor.</p>



<p class="wp-block-paragraph">By using this powerful combination of tools, the WordPress community is moving toward a future where the distinction between &#8220;user&#8221; and &#8220;developer&#8221; continues to blur. This browser-based workflow provides a safe, scalable, and professional way to build the next generation of block themes while maintaining the integrity of version control.</p>



<p class="has-text-align-right wp-block-paragraph"><em>Props to </em><a class="mention" href="https://profiles.wordpress.org/greenshady/"><span class="mentions-prefix">@</span>greenshady</a><em> and <a class="mention" href="https://profiles.wordpress.org/areziaal/"><span class="mentions-prefix">@</span>areziaal</a> for review. </em></p>

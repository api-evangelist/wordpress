---
title: "From Abilities to AI Agents: Introducing the WordPress MCP Adapter"
url: "https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/"
date: "Wed, 04 Feb 2026 14:35:29 +0000"
author: "Jonathan Bossenger"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">The <a href="https://make.wordpress.org/core/2025/11/10/abilities-api-in-wordpress-6-9/">Abilities API introduced in WordPress 6.9</a> makes it possible to register WordPress functionality that is <strong>standardized, discoverable, typed, and executable</strong>. It provides a solid foundation on which WordPress developers can build and extend across the WordPress ecosystem.</p>



<p class="wp-block-paragraph">It&#8217;s also a major step in making WordPress ready for AI automation and workflows. With Abilities, WordPress is positioned to take advantage of any current and future developments in Generative AI.</p>



<p class="wp-block-paragraph">One of the biggest of these recent developments is the <a href="https://modelcontextprotocol.io/docs/getting-started/intro">Model Context Protocol</a>, or MCP.</p>



<p class="wp-block-paragraph">With MCP, it&#8217;s possible to provide additional context to the models which power AI tools. Let&#8217;s say you were using an AI tool to help you draft a report of all sales on your WordPress powered ecommerce site. Imagine if it was possible to give the AI secure access to all your orders for the year. If WordPress supported MCP, it would be.</p>



<p class="wp-block-paragraph">Fortunately, the Core AI team has already thought of this, with the release of the <a href="https://make.wordpress.org/ai/2025/07/17/mcp-adapter/">MCP Adapter</a>. This adapter implements the Model Context Protocol in the scope of a WordPress site and lets AI tools (like Claude Desktop, Claude Code, Cursor, and VS Code) <strong>discover and call WordPress Abilities directly</strong>.</p>



<p class="wp-block-paragraph">So let&#8217;s dive into the MCP Adapter. In this post, you’ll learn:</p>



<ul class="wp-block-list">
<li>How to install and use the MCP Adapter in your WordPress plugins.</li>



<li>How to expose existing abilities as MCP tools<strong>,</strong> with practical examples<strong>.</strong></li>



<li>How to connect popular AI clients to your WordPress-enabled MCP sites, whether local development environments or publicly accessible installs, to interact with your custom MCP tools.</li>



<li>What security considerations you need to be aware of.</li>



<li>How to start experimenting with the MCP adapter right away.</li>
</ul>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#quick-recap-abilities-as-the-foundation">Quick recap: Abilities as the foundation</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#what-is-the-wordpress-mcp-adapter">What is the WordPress MCP Adapter?</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#a-primer-on-mcp-tools-resources-and-prompts">A primer on MCP tools, resources, and prompts</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#installing-the-mcp-adapter">Installing the MCP Adapter</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#enabling-abilities-for-the-mcp-adapter-default-server">Enabling Abilities for the MCP Adapter default server</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#connecting-ai-applications">Connecting AI applications</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#transport-methods">Transport methods</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#app-specific-configurations">App-specific configurations</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#claude-desktop">Claude Desktop</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#cursor">Cursor</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#claude-code">Claude Code</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#vs-code">VS Code</a></li></ol></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#using-mcp-tools">Using MCP tools</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#configuring-custom-mcp-servers-for-your-plugins">Configuring custom MCP Servers for your plugins</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#adding-an-mcp-server-to-list-all-urls">Adding an MCP server to List All URLs</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#security-and-best-practices">Security and best practices</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/02/from-abilities-to-ai-agents-introducing-the-wordpress-mcp-adapter/#how-to-start-experimenting-today">How to start experimenting today</a></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="quick-recap-abilities-as-the-foundation">Quick recap: Abilities as the foundation</h2>



<p class="wp-block-paragraph">If this is the first time you&#8217;re reading about WordPress Abilities, it might be worthwhile to read the Introducing the <a href="https://developer.wordpress.org/news/2025/11/introducing-the-wordpress-abilities-api/">WordPress Abilities API</a> post. However, if you don&#8217;t have the time to read that, here&#8217;s a quick recap.</p>



<p class="wp-block-paragraph">The Abilities API gives WordPress a <strong>first-class, cross-context functional API</strong> that standardizes how core and plugins expose what they can do.</p>



<p class="wp-block-paragraph">You define an ability once with:</p>



<ul class="wp-block-list">
<li>A unique name (<code>namespace/ability-name</code>)</li>



<li>A typed <strong>input schema</strong> and <strong>output schema</strong></li>



<li>A <strong>permission_callback</strong> that enforces capabilities</li>



<li>An <strong>execute_callback</strong> that performs the actual functionality</li>
</ul>



<p class="wp-block-paragraph">The functionality triggered in the <code>execute_callback</code> can be anything from fetching data, updating posts, running diagnostics, or any other discrete unit of work.</p>



<p class="wp-block-paragraph">Once registered, that ability is discoverable and executable from PHP, JavaScript, and the REST API.</p>



<p class="wp-block-paragraph">WordPress 6.9 ships with 3 default abilities:</p>



<ul class="wp-block-list">
<li><code>core/get-site-info</code>: Returns site information configured in WordPress. By default, returns all fields, or optionally a filtered subset.</li>



<li><code>core/get-user-info</code>: Returns basic profile details for the current authenticated user to support personalization, auditing, and access-aware behavior.</li>



<li><code>core/get-environment-info</code>: Returns core details about the site&#8217;s runtime context for diagnostics and compatibility (environment, PHP runtime, database server info, WordPress version).</li>
</ul>



<p class="wp-block-paragraph">While only a small set of Core Abilities, they provide a foundation you can use to test the MCP adapter.</p>



<h2 class="wp-block-heading" id="what-is-the-wordpress-mcp-adapter">What is the WordPress MCP Adapter?</h2>



<p class="wp-block-paragraph">The <strong>WordPress MCP Adapter</strong> is an official package in the <a href="https://make.wordpress.org/ai/2025/07/17/ai-building-blocks/"><em>AI Building Blocks for WordPress</em></a> initiative. Its job is to adapt Abilities registered by the <strong>Abilities API</strong> into the <a href="https://modelcontextprotocol.io/docs/learn/architecture#primitives">primitives</a> supported by the <strong>Model Context Protocol (MCP)</strong> so that AI agents can discover and execute site functionality as <strong>MCP tools</strong> and read WordPress data as <strong>MCP resources.</strong></p>



<p class="wp-block-paragraph">In practice, this means: <strong>if your code already registers abilities, you are one step away from letting an AI agent use them.</strong></p>



<h3 class="wp-block-heading" id="a-primer-on-mcp-tools-resources-and-prompts">A primer on MCP tools, resources, and prompts</h3>



<p class="wp-block-paragraph">The Model Context Protocol organizes interactions into three main primitives: <strong>tools</strong>, which are executable functions the AI calls to perform actions; <strong>resources</strong>, which are passive data sources (like files or database rows) the AI reads for context; and <strong>prompts</strong>, which are pre-configured templates to guide specific workflows.</p>



<p class="wp-block-paragraph">With the MCP adapter, Abilities are generally exposed as <strong>tools</strong> because they represent executable logic—fetching data, updating posts, or running diagnostics. However, the adapter is flexible: if an Ability simply provides read-only data, such as a debug log or a static site configuration, it can also be configured as a <strong>resource</strong>, allowing the AI to ingest that information as background context without needing to actively &#8220;call&#8221; it.</p>



<h2 class="wp-block-heading" id="installing-the-mcp-adapter">Installing the MCP Adapter</h2>



<p class="wp-block-paragraph">The quickest way to get started with the MCP Adapter is to download and install it as a plugin from the <a href="https://github.com/WordPress/mcp-adapter/releases">Releases page of the GitHub repository</a>.</p>



<p class="wp-block-paragraph">Once the plugin is installed and activated, it will register a <strong>default MCP server</strong> named <code>mcp-adapter-default-server</code>, and three custom abilities.</p>



<ul class="wp-block-list">
<li><code>mcp-adapter/discover-abilities</code></li>



<li><code>mcp-adapter/get-ability-info</code></li>



<li><code>mcp-adapter/execute-ability</code></li>
</ul>



<p class="wp-block-paragraph">These abilities are also automatically exposed as MCP tools:</p>



<ul class="wp-block-list">
<li><code>mcp-adapter-discover-abilities</code></li>



<li><code>mcp-adapter-get-ability-info</code></li>



<li><code>mcp-adapter-execute-ability</code></li>
</ul>



<p class="wp-block-paragraph">These three tools offer AI agents a <a href="https://engineering.block.xyz/blog/build-mcp-tools-like-ogres-with-layers">layered approach</a> to accessing WordPress Abilities. Agents can <strong>discover</strong> which Abilities are available, <strong>get</strong> ability information, and <strong>execute</strong> abilities.</p>



<h2 class="wp-block-heading" id="enabling-abilities-for-the-mcp-adapter-default-server">Enabling Abilities for the MCP Adapter default server</h2>



<p class="wp-block-paragraph">By default, Abilities are only available via the MCP Adapter default server if they are explicitly marked as public for MCP access. For this, you need to add a <code>meta.mcp.public</code> flag to the ability registration arguments when you register your ability with <code>wp_register_ability()</code>.</p>



<pre class="wp-block-code"><code class="language-php" lang="php">'meta' =&gt; array(
    'mcp' =&gt; array(
        'public' =&gt; true,  // Required for MCP default server access
    ),
)</code></pre>



<p class="wp-block-paragraph">In the case of any Core Abilities, you can hook into the <code>wp_register_ability_args</code> filter to update their registration arguments to include the <code>meta.mcp.public</code> flag.</p>



<pre class="wp-block-code"><code class="language-php" lang="php">&lt;?php
/**
 * Plugin Name: Enable core abilities
 * Version: 1.0.0
 *
 * @package enable-core-abilities
 */

add_filter( 'wp_register_ability_args', 'myplugin_enable_core_abilities_mcp_access', 10, 2 );
/**
 * Enable MCP access for core abilities.
 *
 * @param array  $args        Ability registration arguments.
 * @param string $ability_name  Ability ID.
 * @return array Modified ability registration arguments.
 */
function myplugin_enable_core_abilities_mcp_access( array $args, string $ability_name ) {
    // Enable MCP access for the three current core abilities.
    $core_abilities = array(
        'core/get-site-info',
        'core/get-user-info',
        'core/get-environment-info',
    );
    if ( in_array( $ability_name, $core_abilities, true ) ) {
        $args['meta']['mcp']['public'] = true;
    }

    return $args;
}</code></pre>



<p class="wp-block-paragraph">With this in place, you can start connecting AI clients to your WordPress site via the MCP Adapter and start calling these core abilities via the default server&#8217;s MCP tools.</p>



<h2 class="wp-block-heading" id="connecting-ai-applications">Connecting AI applications</h2>



<h3 class="wp-block-heading" id="transport-methods">Transport methods</h3>



<p class="wp-block-paragraph">To communicate with a WordPress site that’s enabled as an MCP server, there are <a href="https://modelcontextprotocol.io/docs/learn/architecture#transport-layer">two transport mechanisms</a>: <strong>STDIO</strong> and <strong>HTTP</strong>. Which one you use is generally decided by where the WordPress site is located.</p>



<p class="wp-block-paragraph">For local WordPress development environments, the most straightforward way to connect is using <strong>STDIO</strong> transport. The MCP Adapter makes this possible via <a href="https://wp-cli.org/">WP-CLI</a>, so you need to have WP-CLI installed locally.</p>



<p class="wp-block-paragraph">For the STDIO transport, at minimum you need to configure the following to connect to your MCP enabled WordPress site:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">   "wordpress-mcp-server": {
      "command": "wp",
      "args": [
        "--path=/path/to/your/wordpress/installation",
        "mcp-adapter",
        "serve",
        "--server=mcp-adapter-default-server",
        "--user={admin_user}"
      ]
    }</code></pre>



<ul class="wp-block-list">
<li>the server name in this case is <code>wordpress-mcp-server</code>. This can be any name you choose.</li>



<li>the command is <code>wp</code>, which is the WP-CLI command-line tool</li>



<li>the args array includes:</li>



<li><code>--path</code> pointing to your WordPress installation</li>



<li><code>mcp-adapter serve</code> to start the MCP Adapter server</li>



<li><code>--server</code> specifying the MCP server to use (in this case, the default server)</li>



<li><code>--user</code> specifying the WordPress user to authenticate as (in this case the <code>admin</code> user)</li>
</ul>



<p class="wp-block-paragraph">For any publicly accessible WordPress installations, or if you don&#8217;t want to use STDIO, you can set up an <strong>HTTP</strong> connection using the <a href="https://www.npmjs.com/package/@automattic/mcp-wordpress-remote"><code>@automattic/mcp-wordpress-remote</code></a> remote proxy. This requires you to have <a href="https://nodejs.org/en">Node.js</a> installed on your computer, and to set up authentication using either <a href="https://make.wordpress.org/core/2020/11/05/application-passwords-integration-guide/">WordPress application passwords</a> or a custom OAuth implementation.</p>



<p class="wp-block-paragraph">If you&#8217;re using the HTTP transport, your minimum configuration should look like this:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">   "wordpress-mcp-server": {
      "command": "npx",
      "args": ["-y", "@automattic/mcp-wordpress-remote@latest"],
      "env": {
        "WP_API_URL": "https://yoursite.example/wp-json/mcp/mcp-adapter-default-server",
        "WP_API_USERNAME": "{admin_user}",
        "WP_API_PASSWORD": "{application-password}"
      }
    }</code></pre>



<ul class="wp-block-list">
<li>the server name stays the same</li>



<li>the command is <code>npx</code>, which executes Node.js packages</li>



<li>the args array includes:</li>



<li><code>-y</code> to automatically agree to install the package</li>



<li><code>@automattic/mcp-wordpress-remote@latest</code> to use the latest version of the remote MCP proxy package</li>



<li>the env object includes:</li>



<li><code>WP_API_URL</code> pointing to the MCP endpoint on your WordPress site</li>



<li><code>WP_API_USERNAME</code> specifying the WordPress user to authenticate as</li>



<li><code>WP_API_PASSWORD</code> specifying the application password for the user</li>
</ul>



<p class="wp-block-paragraph">For local WordPress installations connecting via the HTTP remote proxy, the <code>mcp-wordpress-remote</code> package <a href="https://github.com/Automattic/mcp-wordpress-remote/blob/trunk/Docs/troubleshooting.md">includes some troubleshooting tips</a> if you run into any issues connecting. Usually, these issues are related to having multiple versions of Node.js installed or issues related to local SSL certificates.</p>



<h3 class="wp-block-heading" id="app-specific-configurations">App-specific configurations</h3>



<p class="wp-block-paragraph">Now let&#8217;s look at where to configure your MCP server in the most popular AI applications, Claude Desktop, VS Code, Cursor, and Claude Code.</p>



<p class="wp-block-paragraph"><strong>Note:</strong> For all the examples below, I&#8217;m using a Studio site named &#8216;WordPress MCP&#8217; located at <code>/Users/jonathanbossenger/Studio/wordpress-mcp</code> and browsable via <a href="http://localhost:8885/">http://localhost:8885/</a>, with an admin user named <code>admin</code>. Make sure to replace these values with your own WordPress site path and user.</p>



<h4 class="wp-block-heading" id="claude-desktop">Claude Desktop</h4>



<p class="wp-block-paragraph">Being an Anthropic product, Claude Desktop was one of the first apps with built-in support for MCP servers. To add MCP servers to Claude Desktop, navigate to the <strong>Developer</strong> tab (<em>Claude <span class="wp-exclude-emoji">→</span> Settings <span class="wp-exclude-emoji">→</span> Developer</em>). Under Local MCP servers click <strong>Edit config</strong>.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Claude desktop developer settings panel" class="wp-image-5830" height="1822" src="https://developer.wordpress.org/news/files/2026/02/mcp-01-claude-developer-settings.png" width="2726" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">This will open a file browser to the location of the <code>claude_desktop_config.json</code> file, where you can add your MCP server configurations.</p>



<p class="wp-block-paragraph">MCP Servers are added to this file in a <code>mcpServers</code> object.</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "mcpServers": {
  }
}</code></pre>



<p class="wp-block-paragraph">Here&#8217;s what the configuration looks like for connecting via STDIO transport:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "mcpServers": {
    "wordpress-mcp-server": {
      "command": "wp",
      "args": [
        "--path=/Users/jonathanbossenger/Studio/wordpress-mcp",
        "mcp-adapter",
        "serve",
        "--server=mcp-adapter-default-server",
        "--user=admin"
      ]
    }
  }
}</code></pre>



<p class="wp-block-paragraph">Here&#8217;s what the configuration looks like for connecting via HTTP transport:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "mcpServers": {
    "wordpress-mcp-server": {
      "command": "npx",
      "args": ["-y", "@automattic/mcp-wordpress-remote@latest"],
      "env": {
        "WP_API_URL": "http://localhost:8885/wp-json/mcp/mcp-adapter-default-server",
        "WP_API_USERNAME": "admin",
        "WP_API_PASSWORD": "2SEB qW5j D7CW fpsh pbmN RGva"
      }
    }
  }
}</code></pre>



<p class="wp-block-paragraph">Once you save the configuration file, you will have to restart Claude Desktop, as it only reads the MCP server configurations on startup.</p>



<p class="wp-block-paragraph">You should now see your MCP server listed in the <strong>Developer</strong> tab under <strong>Local MCP servers</strong>. If you see the <code>running</code> status next to your server name, you&#8217;re ready to start using it in your conversations.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Claude desktop developer settings panel with WordPress MCP server added." class="wp-image-5831" height="1822" src="https://developer.wordpress.org/news/files/2026/02/mcp-02-claude-mcp-server.png" width="2726" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h4 class="wp-block-heading" id="cursor">Cursor</h4>



<p class="wp-block-paragraph">In Cursor, navigate to the <strong>Settings</strong> tab (<em>Cursor <span class="wp-exclude-emoji">→</span> Settings <span class="wp-exclude-emoji">→</span> Cursor Settings</em>), then select the <strong>Tools and MCP</strong> section.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Cursor Tools &amp; MCP settings panel" class="wp-image-5833" height="1874" src="https://developer.wordpress.org/news/files/2026/02/mcp-04-cursor.png" width="2992" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">Click on <strong>Add Custom MCP</strong> button, which will open the <code>mcp.json</code> configuration file for Cursor.</p>



<p class="wp-block-paragraph">The configuration for Cursor is the same as for Claude Desktop. Once you&#8217;ve added your MCP server configuration, save the file and navigate back to the <strong>Tools and MCP</strong> section in Cursor settings. You should see your MCP server listed there, and you can enable it for use in your coding sessions.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Cursor Tools &amp; MCP settings panel with WordPress MCP Server added." class="wp-image-5834" height="1874" src="https://developer.wordpress.org/news/files/2026/02/mcp-05-cursor-mcp.png" width="2992" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h4 class="wp-block-heading" id="claude-code">Claude Code</h4>



<p class="wp-block-paragraph">To add MCP servers to Claude Code, you can either add the <code>mcpServers</code> object with the relevant server configs to the <code>.claude.json</code> file in your home directory, or create a <code>.mcp.json</code> file in your project directory. Adding the MCP servers to the project directory allows you to have different MCP server configurations for different projects, whereas adding them to the home directory makes them available globally across all projects.</p>



<p class="wp-block-paragraph">Either way, you can use the same configuration format as Cursor or Claude Desktop.</p>



<h4 class="wp-block-heading" id="vs-code">VS Code</h4>



<p class="wp-block-paragraph">Configuring VS Code to connect to an MCP server requires setting up a <a href="https://code.visualstudio.com/docs/copilot/customization/mcp-servers">JSON configuration file that describes the MCP server details</a>. This file is usually named <code>mcp.json</code> and should be placed in a <code>.vscode</code> directory inside your project workspace.</p>



<p class="wp-block-paragraph">The only difference between configuring VS Code and Claude Desktop is that you define your MCP servers in a <code>servers</code> object not an <code>mcpServers</code> object. The rest of the configuration is the same.</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "servers": {
    // MCP server definitions go here
  }
}</code></pre>



<p class="wp-block-paragraph">Once you create this file in your project workspace, VS Code displays an MCP control toolbar, where you can start, stop and restart the MCP server.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="VSCode mcp.json file with MCP JSON configuration for WordPress MCP server." class="wp-image-5835" height="1910" src="https://developer.wordpress.org/news/files/2026/02/mcp-06-vscode.png" width="2998" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">When the server has started correctly, it will also show you how many tools are available for the AI to use, in this case, three.</p>



<h2 class="wp-block-heading" id="using-mcp-tools">Using MCP tools</h2>



<p class="wp-block-paragraph">With your MCP server connected to your AI application of choice, you can now start using the MCP tools exposed by the MCP Adapter.</p>



<p class="wp-block-paragraph">For example, in Claude Desktop, you can start a new conversation asking Claude to &#8220;Get the site info from my WordPress site&#8221;.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="Claude desktop AI Query showing results from WordPress MCP server." class="wp-image-5832" height="1822" src="https://developer.wordpress.org/news/files/2026/02/mcp-03-claude-query.png" width="2726" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">It will determine that there is an available MCP server and call the <code>mcp-adapter-discover-abilities</code> tool to see what abilities are available. It will then determine that the <code>core/get-site-info</code> Ability will fulfill the request, and call the <code>mcp-adapter-execute-ability</code> tool, passing it the <code>core/get-site-info</code> Ability name. This will return the site info data, and the application will &#8220;answer&#8221; with the site information.</p>



<h2 class="wp-block-heading" id="configuring-custom-mcp-servers-for-your-plugins">Configuring custom MCP Servers for your plugins</h2>



<p class="wp-block-paragraph">While the MCP Adapter default server should cover most requirements, you may want to create a custom MCP server for your plugin. This allows you to have more control over how your abilities are exposed as MCP tools.</p>



<p class="wp-block-paragraph">Implementing this requires installing the MCP Adapter package via Composer, and creating and registering a custom MCP server.</p>



<p class="wp-block-paragraph">From your plugin directory, run the <code>composer require</code> command:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">composer require wordpress/mcp-adapter</code></pre>



<p class="wp-block-paragraph">Then, make sure to load Composer’s autoloader in your main plugin file:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">if ( file_exists( __DIR__ . '/vendor/autoload.php' ) ) {
    require_once __DIR__ . '/vendor/autoload.php';
}</code></pre>



<p class="wp-block-paragraph">If it&#8217;s possible that multiple plugins on a site might depend on the MCP Adapter or Abilities API, the official documentation <a href="https://github.com/WordPress/mcp-adapter/blob/trunk/docs/getting-started/installation.md#using-jetpack-autoloader-highly-recommended">recommends using the Jetpack Autoloader</a> to avoid version conflicts.</p>



<p class="wp-block-paragraph">The next step is to initialize the MCP Adapter in your plugin:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">if ( ! class_exists( WP\MCP\Core\McpAdapter::class ) ) {
    // check if the MCP Adapter class is available, if not show some sort of error or admin notice
    return;
}

// Initialize MCP Adapter and its default server.
WP\MCP\Core\McpAdapter::instance();</code></pre>



<p class="wp-block-paragraph">Finally, you can create a custom MCP server by hooking into the <code>mcp_adapter_init</code> action. The action callback function receives the <code>McpAdapter</code> instance. The adapter&#8217;s <code>create_server()</code> method is used to define the custom server, with the desired configuration.</p>



<pre class="wp-block-code"><code class="language-php" lang="php">add_action( 'mcp_adapter_init', 'myplugin_create_custom_mcp_server' );
function myplugin_create_custom_mcp_server( $adapter ) {
    $adapter = WP\MCP\Core\McpAdapter::instance();
    $adapter-&gt;create_server(
        'custom-mcp-server', // Unique server identifier.
        'custom-mcp-server', // REST API namespace.
        'mcp',               // REST API route.
        'Custom MCP Server', // Server name.
        'Custom MCP Server', // Server description.
        'v1.0.0',            // Server version.
        array(               // Transport methods.
            \WP\MCP\Transport\HttpTransport::class,  // Recommended: MCP 2025-06-18 compliant.
        ),
        \WP\MCP\Infrastructure\ErrorHandling\ErrorLogMcpErrorHandler::class, // Error handler.
        \WP\MCP\Infrastructure\Observability\NullMcpObservabilityHandler::class, // Observability handler.
        array( 'namespace/ability-name' ), // Abilities to expose as tools
        array(),                           // Resources (optional).
        array(),                           // Prompts (optional).
    );
}</code></pre>



<p class="wp-block-paragraph">The important parameters to note here are:</p>



<ul class="wp-block-list">
<li>The first parameter is the unique server identifier. This is used when starting the MCP server via WP-CLI.</li>



<li>The second and third parameters define the REST API namespace and route for the MCP server.</li>



<li>The fourth and fifth parameters are the server name and description, which are displayed in AI applications when listing available MCP servers.</li>



<li>The sixth parameter is the server version.</li>



<li>The tenth parameter is an array of ability names that you want to expose as MCP tools. You can list multiple abilities here.</li>



<li>The rest of the parameters define the transport methods, error handling, and observability handlers. In this example, you&#8217;re using the HTTP transport, error logging, and observability handlers from the core MCP Adapter package. However, it is possible to create your own custom handlers if you want to integrate with your own transport, logging or monitoring systems.</li>
</ul>



<h2 class="wp-block-heading" id="adding-an-mcp-server-to-list-all-urls">Adding an MCP server to List All URLs</h2>



<p class="wp-block-paragraph">To show you an example of creating a custom MCP server, let&#8217;s take the <a href="https://github.com/wptrainingteam/list-all-urls">List All URLs plugin</a> from the Abilities API post, and add a custom MCP server to it.</p>



<p class="wp-block-paragraph">Before you do this, deactivate the MCP Adapter plugin if you have it activated.</p>



<p class="wp-block-paragraph">Next, clone the List All URLs GitHub repository inside your WordPress plugins directory:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">cd wp-content/plugins
git clone git@github.com:wptrainingteam/list-all-urls.git</code></pre>



<p class="wp-block-paragraph">You&#8217;ll also need to switch to the branch that includes the Abilities API implementation:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">cd list-all-urls
git checkout abilities</code></pre>



<p class="wp-block-paragraph">The plugin already uses Composer for dependency management, so run <code>composer install</code> to install the required packages.</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">composer install</code></pre>



<p class="wp-block-paragraph">Next require the mcp-adapter package:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">composer require wordpress/mcp-adapter</code></pre>



<p class="wp-block-paragraph">Now, open the main plugin file <code>list-all-urls.php</code>, and add the following code at the bottom of the file to initialize the MCP Adapter and create a custom MCP server:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">if ( ! class_exists( WP\MCP\Core\McpAdapter::class ) ) {
    return;
}

// Initialize MCP Adapter and its default server.
WP\MCP\Core\McpAdapter::instance();

add_action( 'mcp_adapter_init', 'list_all_urls_create_custom_mcp_server' );
/**
 * Create a custom MCP server for the List All URLs plugin.
 *
 * @param object $adapter WP\MCP\Core\McpAdapter The MCP Adapter instance.
 * @return void
 */
function list_all_urls_create_custom_mcp_server( $adapter ) {
    $adapter = WP\MCP\Core\McpAdapter::instance();
    $adapter-&gt;create_server(
        'list-all-urls-mcp-server',
        'list-all-urls-mcp-server',
        'mcp',
        'List All URLS MCP Server',
        'Custom MCP Server for the List All URLs plugin. Currently exposes only the list-all-urls/urls ability as an MCP Tool.',
        'v1.0.0',
        array(
            \WP\MCP\Transport\HttpTransport::class,
        ),
        \WP\MCP\Infrastructure\ErrorHandling\ErrorLogMcpErrorHandler::class,
        \WP\MCP\Infrastructure\Observability\NullMcpObservabilityHandler::class,
        array( 'list-all-urls/urls' ),
    );
}</code></pre>



<p class="wp-block-paragraph">Notice that you don&#8217;t need to enable the <code>meta.mcp.public</code> flag for the <code>list-all-urls/urls</code> ability, because you&#8217;re explicitly exposing it via the custom MCP server.</p>



<p class="wp-block-paragraph">Now activate the List All URLs plugin from the WordPress admin dashboard.</p>



<p class="wp-block-paragraph">Once the plugin is activated, update your AI application&#8217;s MCP server configuration to use the new custom MCP server.</p>



<p class="wp-block-paragraph">Here&#8217;s an example of the updated VS Code configuration to include both the default MCP server and the new custom MCP server from the List All URLs plugin, both using STDIO transport:</p>



<pre class="wp-block-code"><code class="language-json" lang="json">{
  "servers": {
    "wordpress-mcp-server": {
      "command": "wp",
      "args": [
        "--path=/Users/jonathanbossenger/Studio/wordpress-mcp",
        "mcp-adapter",
        "serve",
        "--server=mcp-adapter-default-server",
        "--user=admin"
      ]
    },
    "list-all-urls-mcp-server": {
      "command": "wp",
      "args": [
        "--path=/Users/jonathanbossenger/Studio/wordpress-mcp",
        "mcp-adapter",
        "serve",
        "--server=list-all-urls-mcp-server",
        "--user=admin"
      ]
    }
  }
}</code></pre>



<p class="wp-block-paragraph">It&#8217;s possible to have multiple MCP servers configured in the same AI application. This allows you to switch between different WordPress sites or plugins that expose different sets of abilities.</p>



<p class="wp-block-paragraph">Whatever AI application you&#8217;re using, make sure to either restart the application, or start the MCP server in the application after updating the MCP server configuration. You should see the new MCP server listed and be able to use the <code>list-all-urls/urls</code> ability as an MCP tool. You can then ask the AI to &#8220;List all URLs on my WordPress site&#8221;, and it will call the <code>list-all-urls-urls</code> tool via the MCP Adapter.</p>



<figure class="wp-block-image size-full wp-lightbox-container"><img alt="VS Code using MCP Tools to query List All URLs data." class="wp-image-5837" height="1910" src="https://developer.wordpress.org/news/files/2026/02/mcp-06-vscode-list-urls.png" width="2998" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h2 class="wp-block-heading" id="security-and-best-practices">Security and best practices</h2>



<p class="wp-block-paragraph">Because MCP clients act as <strong>logged-in WordPress users</strong>, always treat them as part of your application surface area by following these best practices:</p>



<ul class="wp-block-list">
<li><strong>Use <code>permission_callback</code> carefully</strong></li>



<li>Each ability should check the minimum capability needed (<code>manage_options</code>, <code>edit_posts</code>, etc.).</li>



<li>Avoid <code>__return_true</code> for destructive operations such as deleting content.</li>



<li><strong>Use dedicated users for MCP access</strong></li>



<li>Especially in production, create a specific role/user with limited capabilities.</li>



<li>Do not expose powerful abilities to unaudited AI clients.</li>



<li><strong>Prefer read-only abilities for public MCP endpoints</strong></li>



<li>For HTTP transports exposed over the internet, focus on read-only diagnostics, reporting, and content access.</li>



<li><strong>Implement custom authentication if needed</strong></li>



<li>The default authentication uses application passwords, but you can implement OAuth or other methods for better security.</li>



<li><strong>Monitor and log usage</strong></li>



<li>Use custom error and observability handlers to integrate with your logging/monitoring stack.</li>
</ul>



<h2 class="wp-block-heading" id="how-to-start-experimenting-today">How to start experimenting today</h2>



<p class="wp-block-paragraph">If you want to get started experimenting with the MCP adapter, a minimal “hello AI” path for a WordPress developer only requires you to register an ability, require and initialize the MCP Adapter, and connect an MCP-aware AI client.</p>



<p class="wp-block-paragraph">If you already have plugins using the Abilities API, the MCP Adapter turns them into <strong>AI-ready APIs</strong> with very little additional work.</p>



<p class="wp-block-paragraph">As with any new technology, start small. Begin by exposing a few non-destructive, read-only abilities as MCP tools. Test them with local AI clients like Claude Desktop or Cursor. Gradually expand to more complex abilities and workflows as you gain confidence. Be prepared to hit roadblocks, and engage with the WordPress AI and developer communities for support and collaboration. The documentation for both the <a href="https://developer.wordpress.org/apis/abilities/">Abilities API</a> and the <a href="https://github.com/WordPress/mcp-adapter">MCP Adapter</a> are great resources to help you along the way.</p>



<p class="wp-block-paragraph">This combination of Abilities and the MCP Adapter gives WordPress developers a powerful path to build AI-assisted admin tools, automation, and workflows for both clients and teams.</p>



<p class="wp-block-paragraph"><em>Props to <a class="mention" href="https://profiles.wordpress.org/greenshady/"><span class="mentions-prefix">@</span>greenshady</a> and <a class="mention" href="https://profiles.wordpress.org/bph/"><span class="mentions-prefix">@</span>bph</a> for reviewing this post.</em></p>

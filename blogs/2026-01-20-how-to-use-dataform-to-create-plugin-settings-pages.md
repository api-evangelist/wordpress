---
title: "How to use DataForm to create plugin settings pages"
url: "https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/"
date: "Tue, 20 Jan 2026 17:11:57 +0000"
author: "Róbert Mészáros"
feed_url: "https://developer.wordpress.org/news/feed/"
---
<p class="wp-block-paragraph">WordPress is in the midst of an <a href="https://make.wordpress.org/core/2023/07/12/admin-design/">admin redesign</a>. During this transitional phase, the admin consists of two parts: the &#8220;classic&#8221; interface that has been around for over a decade, and the &#8220;modern&#8221; interface that comes with the Block and Site Editor.</p>



<p class="wp-block-paragraph">If you&#8217;re building a plugin that needs a settings page and you want to align with the WordPress Core user experience, it&#8217;s already worth adopting the design elements and patterns that will become the new standard.</p>



<p class="wp-block-paragraph">One way to do this is to use WordPress React components when building settings pages. The <a href="https://developer.wordpress.org/news/2024/03/how-to-use-wordpress-react-components-for-plugin-pages/">How to use WordPress React components for plugin pages</a> article introduced this approach. However, thanks to the work of many in the last year or so, there is a viable alternative approach worth considering and exploring.</p>



<p class="wp-block-paragraph">In this article, you&#8217;ll learn how to rebuild the same settings page that was built using individual React components, but this time using <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/#dataform"><code>DataForm</code></a>. The <code>DataForm</code> component provides a declarative way of creating forms and panels without the need to import individual components.</p>



<p class="wp-block-paragraph">As a preview, here&#8217;s how the settings page currently looks:</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Before refactor" class="wp-image-5765" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-00-b-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">And here&#8217;s the end result after the refactoring is done:</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="After refactor" class="wp-image-5776" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-09-b-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<div class="wp-block-group has-light-grey-2-background-color has-background is-layout-flow wp-block-group-is-layout-flow">
<p class="has-large-font-size wp-block-paragraph" style="font-style: normal; font-weight: 600; line-height: 1;">Table of Contents</p>



<nav class="wp-block-table-of-contents"><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#prerequisites">Prerequisites</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#the-original-settingspage-component">The original SettingsPage component</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#installing-the-wordpress-dataviews-package">Installing the @wordpress/dataviews package</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#adding-the-dataform-component">Adding the DataForm component</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#configuring-form-fields">Configuring form fields</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#adding-the-message-f">Adding the Message field</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#adding-the-display-field">Adding the Display field</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#adding-the-font-size-field">Adding the Font Size field</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#customizing-field-ui-components">Customizing field UI components</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#configuring-the-form-layout">Configuring the form layout</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#grouping-fields-into-sections">Grouping fields into sections</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#switching-the-layout-type">Switching the layout type</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#adjusting-layout-options">Adjusting layout options</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#connecting-dataform-to-the-settings-state">Connecting DataForm to the settings state</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#refactoring-the-usesettings-hook">Refactoring the useSettings hook</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#connecting-the-usesettings-with-dataform">Connecting the useSettings with DataForm</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#implementing-the-onchange-callback">Implementing the onChange callback</a></li></ol></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#wrapping-up">Wrapping up</a><ol><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#try-it-yourself">Try it yourself</a></li><li><a class="wp-block-table-of-contents__entry" href="https://developer.wordpress.org/news/2026/01/how-to-use-dataform-to-create-plugin-settings-pages/#where-to-go-from-here">Where to go from here</a></li></ol></li></ol></nav>
</div>



<h2 class="wp-block-heading" id="prerequisites">Prerequisites</h2>



<p class="wp-block-paragraph">This article assumes you&#8217;ve already read <a href="https://developer.wordpress.org/news/2024/03/how-to-use-wordpress-react-components-for-plugin-pages/">How to use WordPress React components for plugin pages</a> and are familiar with what was built there. If you haven&#8217;t done so, now is a good time!</p>



<p class="wp-block-paragraph">This article doesn&#8217;t cover how to register an admin page, enqueue assets, or register and expose settings via the REST API. All of that was covered in the previous article and remains unchanged.</p>



<p class="wp-block-paragraph">If you want to follow along, you can download or clone the <a href="https://github.com/wptrainingteam/unadorned-announcement-bar">Unadorned Announcement Bar plugin&#8217;s repository</a> as a starting point and follow the setup instructions. The work continues where the previous article left off.</p>



<p class="wp-block-paragraph">If you get stuck at any point, you can compare your changes with the <code>dataform-refactor</code> branch. <a href="https://github.com/wptrainingteam/unadorned-announcement-bar/compare/main...dataform-refactor">Each step is committed separately</a>.</p>



<h2 class="wp-block-heading" id="the-original-settingspage-component">The original <code>SettingsPage</code> component</h2>



<p class="wp-block-paragraph">The “original” settings page component consists of multiple components and a custom hook for managing state.</p>



<p class="wp-block-paragraph">The code for the <code>SettingsPage</code> component looks like this:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    const {
        message,
        setMessage,
        display,
        setDisplay,
        size,
        setSize,
        saveSettings,
    } = useSettings();

    return (
        &lt;&gt;
            &lt;SettingsTitle /&gt;
            &lt;Notices /&gt;
            &lt;Panel&gt;
                &lt;PanelBody&gt;
                    &lt;PanelRow&gt;
                        &lt;MessageControl
                            value={ message }
                            onChange={ ( value ) =&gt; setMessage( value ) }
                        /&gt;
                    &lt;/PanelRow&gt;
                    &lt;PanelRow&gt;
                        &lt;DisplayControl
                            value={ display }
                            onChange={ ( value ) =&gt; setDisplay( value ) }
                        /&gt;
                    &lt;/PanelRow&gt;
                &lt;/PanelBody&gt;
                &lt;PanelBody
                    title={ __( 'Appearance', 'unadorned-announcement-bar' ) }
                    initialOpen={ false }
                &gt;
                    &lt;PanelRow&gt;
                        &lt;SizeControl
                            value={ size }
                            onChange={ ( value ) =&gt; setSize( value ) }
                        /&gt;
                    &lt;/PanelRow&gt;
                &lt;/PanelBody&gt;
            &lt;/Panel&gt;
            &lt;SaveButton onClick={ saveSettings } /&gt;
        &lt;/&gt;
    );
};</code></pre>



<p class="wp-block-paragraph">Everything is built using components from the <a href="https://developer.wordpress.org/block-editor/reference-guides/components/">@wordpress/components</a> package. Even the custom components like <code>MessageControl</code> are simply wrappers around components provided by WordPress:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const MessageControl = ( { value, onChange } ) =&gt; {
    return (
        &lt;TextareaControl
            label={ __( 'Message', 'unadorned-announcement-bar' ) }
            value={ value }
            onChange={ onChange }
            __nextHasNoMarginBottom
        /&gt;
    );
};</code></pre>



<p class="wp-block-paragraph">With <code>DataForm</code>, none of these individual components are needed, only the <code>DataForm</code> itself.</p>



<h2 class="wp-block-heading" id="installing-the-wordpress-dataviews-package">Installing the <code>@wordpress/dataviews</code> package</h2>



<p class="wp-block-paragraph">As a first step, install the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/"><code>@wordpress/dataviews</code></a> package, as the <code>DataForm</code> component is part of it.</p>



<p class="wp-block-paragraph">Run the following command from within the plugin&#8217;s folder:</p>



<pre class="wp-block-code"><code class="language-bash" lang="bash">npm install @wordpress/dataviews --save</code></pre>



<p class="wp-block-paragraph">Next, import <code>DataForm</code> by adding the following to the beginning of your <code>/src/components/settings-page.jsx</code> file:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">import { DataForm } from '@wordpress/dataviews/wp';</code></pre>



<p class="wp-block-paragraph">Currently, when using <code>@wordpress/dataviews</code> in a WordPress context with <code>wp-scripts</code> (as opposed to a standalone application), you must import from <code>@wordpress/dataviews/wp</code> <a href="https://github.com/WordPress/gutenberg/issues/63657#issuecomment-2530638186">to ensure dependencies are resolved correctly</a>.</p>



<h2 class="wp-block-heading" id="adding-the-dataform-component">Adding the <code>DataForm</code> component</h2>



<p class="wp-block-paragraph">Since most of the individual components are not needed in your <code>settings-page.jsx</code> file, you can replace the entire <code>Panel</code> component and its children with the <code>DataForm</code> component:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    const {
        // ...    
    } = useSettings();

    return (
        &lt;&gt;
            &lt;SettingsTitle /&gt;
            &lt;Notices /&gt;
            &lt;DataForm /&gt;
            &lt;SaveButton onClick={ saveSettings } /&gt;
        &lt;/&gt;
    );
};</code></pre>



<p class="wp-block-paragraph"><code>DataForm</code> requires a few props (<code>data</code>, <code>fields</code>, <code>form</code>, <code>onChange</code>), but for now, you can provide empty values to get started. You will see in a moment what they are for.</p>



<p class="wp-block-paragraph">After your changes, <code>settings-page.jsx</code> should look like this:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    const {
        // ...
    } = useSettings();

    const data = {};
    const fields = [];
    const form = {};

    return (
        &lt;&gt;
            &lt;SettingsTitle /&gt;
            &lt;Notices /&gt;
            &lt;DataForm
                data={ data }
                fields={ fields }
                form={ form }
                onChange={ () =&gt; {} }
            /&gt;
            &lt;SaveButton onClick={ saveSettings } /&gt;
        &lt;/&gt;
    );
};</code></pre>



<p class="wp-block-paragraph">While you could keep the prop values inline, using variables makes the code more readable because these values will be multiple lines long.</p>



<p class="wp-block-paragraph">If you refresh the settings page, you should see just the header and the Save button, as if you are starting from a blank slate.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Blanc slate first step" class="wp-image-5766" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-01-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h2 class="wp-block-heading" id="configuring-form-fields">Configuring form fields</h2>



<p class="wp-block-paragraph"><code>DataForm</code> is configuration-driven. To define a field, you need to provide at least an <code>id</code>, a <code>label</code>, and a <code>type</code>.</p>



<p class="wp-block-paragraph">The <code>id</code> is a unique identifier for the field and can be any string. The <code>label</code> is the field&#8217;s name displayed in the UI.</p>



<p class="wp-block-paragraph">The <code>type</code>, among other things, defines what kind of data the field holds. This includes <code>text</code>, <code>integer</code>, <code>boolean</code>, <code>datetime</code>, and others. For the full list, check the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/#type">documentation</a>, as the list grows as the package evolves.</p>



<h3 class="wp-block-heading" id="adding-the-message-f">Adding the Message field</h3>



<p class="wp-block-paragraph" id="adding-the-message-f">For the message field, use the <code>text</code> type since it needs to be a free-form text field.</p>



<p class="wp-block-paragraph" id="adding-the-message-f">To add the configuration, update the <code>fields</code> variable, which will hold the configuration of all fields in <code>settings-page.jsx</code>:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    
    const data = {};
    const fields = [
        {
            id: 'message',
            label: __( 'Message', 'unadorned-announcement-bar' ),
            type: 'text',
        },
    ];
    const form = {};

    // ..
};</code></pre>



<p class="wp-block-paragraph">This defines the field but doesn&#8217;t render it. To actually display the message field, include the field’s <code>id</code> in the <code>form</code> variable:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    
    const data = {};
    const fields = [
        {
            id: 'message',
            // ...
        }
    ];
    const form = {
        fields: [ 'message' ], 
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">Finally, you must define an initial value by updating the <code>data</code> variable. For now, set the <code>message</code> field to an empty string.</p>



<p class="wp-block-paragraph">Here&#8217;s how the updated code in the <code>settings-page.jsx</code> should look:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    
    const data = {
        message: '',
    };
    const fields = [
        {
            id: 'message',
            // ...
        }
    ];
    const form = {
        fields: [ 'message' ],
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">At this point, if you refresh the plugin&#8217;s settings page, you should see a text input rendered.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Screenshot: result of adding a message field" class="wp-image-5767" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-02-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">While it&#8217;s not a textarea like before, you&#8217;ll see how to change that shortly.</p>



<h3 class="wp-block-heading" id="adding-the-display-field">Adding the Display field</h3>



<p class="wp-block-paragraph">You can take the same approach for the display field. This time, use the <code>boolean</code> type instead of the <code>text</code> type because it represents an on/off state.</p>



<p class="wp-block-paragraph">Update the variables in <code>settings-page.jsx</code> as follows:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    
    const data = {
        message: '',
        display: false,
    };
    const fields = [
        {
            id: 'message',
            // ...
        },
        {
            id: 'display',
            label: __( 'Display', 'unadorned-announcement-bar' ),
            type: 'boolean',
        },
    ];
    const form = {
        fields: [ 'message', 'display' ],
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">After refreshing the settings page in your browser, you should see a checkbox field rendered below the message field.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Result of adding a Display field" class="wp-image-5768" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-03-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="adding-the-font-size-field">Adding the Font Size field</h3>



<p class="wp-block-paragraph">The remaining field is for font size. This should allow users to select from predefined options such as small, medium, and others.</p>



<p class="wp-block-paragraph">There&#8217;s no dedicated &#8220;select&#8221; type in <code>DataForm</code>. Instead, use the <code>text</code> type (since the value is stored as a string) and add the optional <code>elements</code> property to define options. When <code>elements</code> is present, <code>DataForm</code> renders a select input instead of a text input.</p>



<p class="wp-block-paragraph">Here&#8217;s how <code>settings-page.jsx</code> should look after the update:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    
    const data = {
        message: '',
        display: false,
        size: 'small',
    };
    const fields = [
        {
            id: 'message',
            // ...
        },
        {
            id: 'display',
            // ...
        },
        {
            id: 'size',
            label: __( 'Font size', 'unadorned-announcement-bar' ),
            type: 'text',
            elements: [
                {
                    value: 'small',
                    label: __( 'Small', 'unadorned-announcement-bar' ),
                },
                {
                    value: 'medium',
                    label: __( 'Medium', 'unadorned-announcement-bar' ),
                },
                {
                    value: 'large',
                    label: __( 'Large', 'unadorned-announcement-bar' ),
                },
                {
                    value: 'x-large',
                    label: __( 'Extra Large', 'unadorned-announcement-bar' ),
                },
            ]
        }
    ];
    const form = {
        fields: [ 'message', 'display', 'size' ],
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">With this, your settings page should have three fields without needing to import any specific components, all defined through configuration objects.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Screenshot: Adding a Font size field" class="wp-image-5769" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-04-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="customizing-field-ui-components">Customizing field UI components</h3>



<p class="wp-block-paragraph">When you specify a <code>type</code> for a field without extra configuration, each type maps to a default UI component.</p>



<p class="wp-block-paragraph">As you saw, the <code>text</code> type renders a text input when no elements are defined. The <code>boolean</code> renders a checkbox.</p>



<p class="wp-block-paragraph">However, you can change the default UI components by specifying the <code>Edit</code> property. The simplest option is to use one of the predefined UI components: <code>textarea</code>, <code>toggle</code>, <code>radio</code>, <code>toggleGroup</code>, and others.</p>



<p class="wp-block-paragraph">To complete this, add the <code>Edit</code> property to the fields in <code>settings-page.jsx</code> as follows:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    const fields = [
        {
            id: 'message',
            // ...
            Edit: 'textarea',
        },
        {
            id: 'display',
            // ...
            Edit: 'toggle',
        },
        {
            id: 'size',
            // ...
            Edit: 'toggleGroup',
        },
    ];
    // ..
};</code></pre>



<p class="wp-block-paragraph">Now, if you refresh the settings page, you should see a textarea, a toggle, and a toggle group for the fields.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Screenshot: Customizing field UI omponents" class="wp-image-5770" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-05-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">If you need more than the built-in UI components, you can use your own custom components instead. This allows you to drive your settings page using configuration without being limited by what UI components are available.</p>



<p class="wp-block-paragraph">Refer to the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/#edit">documentation</a> to see how to do that and what built-in components are available today. New components are added over time!</p>



<h2 class="wp-block-heading" id="configuring-the-form-layout">Configuring the form layout</h2>



<p class="wp-block-paragraph">At this point, you have the same controls as before, but the layout is different. The fields aren&#8217;t grouped under panels, and the font size control isn&#8217;t hidden by default.</p>



<p class="wp-block-paragraph"><code>DataForm</code> not only allows you to define fields using a configuration, but also lets you configure the overall layout used to display them.</p>



<h3 class="wp-block-heading" id="grouping-fields-into-sections">Grouping fields into sections</h3>



<p class="wp-block-paragraph">To recreate the previous layout, group the fields into different sections. To achieve that, update the <code>form</code> variable in <code>settings-page.jsx</code> as follows:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    const form = {
        fields: [
            {
                id: 'bar',
                label: __( 'Bar', 'unadorned-announcement-bar' ),
                children: [ 'message', 'display' ],
            },
            {
                id: 'appearance',
                label: __( 'Appearance', 'unadorned-announcement-bar' ),
                children: [ 'size' ],
            },
        ],
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">The configuration requires an <code>id</code> and a <code>label</code>, just like a field definition. However, instead of defining a <code>type</code>, you assign existing fields as <code>children</code>.</p>



<p class="wp-block-paragraph" id="grouping">If you refresh the settings, you can see the fields grouped into two sections. </p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Screenshot: fields grouped into Bar and Appearance sections." class="wp-image-5771" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-06-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="switching-the-layout-type">Switching the layout type</h3>



<p class="wp-block-paragraph">By default, DataForm uses the <code>regular</code> layout, which is the implicit one, which lays out the fields one under the other in separate rows. However, there are other layouts available: <code>panel</code>, <code>card</code>, and <code>row</code>.</p>



<p class="wp-block-paragraph">The card layout gets you closest to the &#8220;original design&#8221;, but try the other layouts as well to see how they look!</p>



<p class="wp-block-paragraph">To switch to the card layout, update the configuration of the <code>form</code> in the <code>settings-page.jsx</code> as follows:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    const form = {
        fields: [
            {
                id: 'bar',
                // ...
                layout: { type: 'card' },
            },
            {
                id: 'appearance',
                // ...
                layout: { type: 'card' },
            },
        ],
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">If it works for you, you can even mix and match layout types for each group separately, allowing you to create various combinations.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Screenshot: Switching the layout type to &apos;card&apos;" class="wp-image-5772" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-07-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<h3 class="wp-block-heading" id="adjusting-layout-options">Adjusting layout options</h3>



<p class="wp-block-paragraph">Depending on the layout, you can specify additional settings.</p>



<p class="wp-block-paragraph">For example, for the <code>card</code> layout, you can control whether a header is displayed or if the card itself is expanded or collapsed by default. To see all the options for each type, check the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/#layout">documentation</a>.</p>



<p class="wp-block-paragraph">To remove the header from the first group and make the second group collapsed by default, modify the <code>layout</code> configuration as follows:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...
    const form = {
        fields: [
            {
                id: 'bar',
                // ...
                layout: { type: 'card', withHeader: false },
            },
            {
                id: 'appearance',
                // ...
                layout: { type: 'card', isOpened: false },
            },
        ],
    };

    // ..
};</code></pre>



<p class="wp-block-paragraph">With this change, if you refresh the settings page, the UI matches very closely to what existed before.</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="Screenshot: modify &apos;card&apos; layout type" class="wp-image-5773" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-08-a-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">The spacing and width of some elements still need minor tweaks, but these can be addressed with the use of <a href="https://developer.wordpress.org/block-editor/reference-guides/components/v-stack/">VStack</a> and custom CSS.</p>



<p class="wp-block-paragraph">With just a few lines, you can polish these details to achieve the final result:</p>



<figure class="wp-block-image alignwide size-large wp-lightbox-container"><img alt="" class="wp-image-5776" height="640" src="https://developer.wordpress.org/news/files/2026/01/how-to-use-dataform-to-create-plugin-settings-pages-09-b-1024x640.png" width="1024" /><button class="lightbox-trigger" type="button">
			<svg fill="none" height="12" viewBox="0 0 12 12" width="12" xmlns="http://www.w3.org/2000/svg">
				<path d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" fill="#fff">
			</svg>
		</button></figure>



<p class="wp-block-paragraph">Since writing CSS is outside the overall scope of this article, <a href="https://github.com/wptrainingteam/unadorned-announcement-bar/commit/bd43f75fe68ce9b8e6ed51e98057aa3a72413afd">refer to the GitHub repository</a> to see how it was implemented.</p>



<h2 class="wp-block-heading" id="connecting-dataform-to-the-settings-state">Connecting <code>DataForm</code> to the <code>settings</code> state</h2>



<p class="wp-block-paragraph">The settings page is rendered, however it&#8217;s still using hardcoded <code>data</code> that&#8217;s passed to the <code>DataForm</code>, and the <code>onChange</code> is not yet implemented:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    const {
        // ...
    } = useSettings();

    const data = {
        message: '',
        display: false,
        size: 'small',
    };
    // ...

    return (
        &lt;&gt;
            &lt;SettingsTitle /&gt;
            &lt;Notices /&gt;
            &lt;DataForm
                data={ data }
                fields={ fields }
                form={ form }
                onChange={ () =&gt; {} }
            /&gt;
            &lt;SaveButton onClick={ saveSettings } /&gt;
        &lt;/&gt;
    );
};</code></pre>



<p class="wp-block-paragraph">The final step is to connect the <code>DataForm</code> with the <code>useSettings</code> custom hook, which handles state management.</p>



<h3 class="wp-block-heading" id="refactoring-the-usesettings-hook">Refactoring the <code>useSettings</code> hook</h3>



<p class="wp-block-paragraph">Currently, the state of fields is stored separately using three <code>useState</code> calls, but the actual settings are fetched and saved as an object under the <code>unadorned_announcement_bar</code> key.</p>



<p class="wp-block-paragraph">As a reference, here&#8217;s the code for the current custom hook in <code>/src/hooks/use-settings.js</code>:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const useSettings = () =&gt; {
    const [ message, setMessage ] = useState();
    const [ display, setDisplay ] = useState();
    const [ size, setSize ] = useState();

    const { createSuccessNotice } = useDispatch( noticesStore );

    useEffect( () =&gt; {
        apiFetch( { path: '/wp/v2/settings' } ).then( ( wpSettings ) =&gt; {
            setMessage( wpSettings.unadorned_announcement_bar.message );
            setDisplay( wpSettings.unadorned_announcement_bar.display );
            setSize( wpSettings.unadorned_announcement_bar.size );
        } );
    }, [] );

    const saveSettings = () =&gt; {
        apiFetch( {
            path: '/wp/v2/settings',
            method: 'POST',
            data: {
                unadorned_announcement_bar: {
                    message,
                    display,
                    size,
                },
            },
        } ).then( () =&gt; {
            createSuccessNotice(
                __( 'Settings saved.', 'unadorned-announcement-bar' )
            );
        } );
    };

    return {
        message,
        setMessage,
        display,
        setDisplay,
        size,
        setSize,
        saveSettings,
    };
};</code></pre>



<p class="wp-block-paragraph">The setting is registered on the server side and has some default values and its schema defined. For reference, here&#8217;s how it was registered:</p>



<pre class="wp-block-code"><code class="language-php" lang="php">function unadorned_announcement_bar_settings() {
    $default = array(
        'message' =&gt; __( 'Hello, World!', 'unadorned-announcement-bar' ),
        'display' =&gt; true,
        'size'    =&gt; 'medium',
    );
    $schema  = array(
        'type'       =&gt; 'object',
        'properties' =&gt; array(
            'message' =&gt; array(
                'type' =&gt; 'string',
            ),
            'display' =&gt; array(
                'type' =&gt; 'boolean',
            ),
            'size'    =&gt; array(
                'type' =&gt; 'string',
                'enum' =&gt; array(
                    'small',
                    'medium',
                    'large',
                    'x-large',
                ),
            ),
        ),
    );

    register_setting(
        'options',
        'unadorned_announcement_bar',
        array(
            'type'         =&gt; 'object',
            'default'      =&gt; $default,
            'show_in_rest' =&gt; array(
                'schema' =&gt; $schema,
            ),
        )
    );
}

add_action( 'init', 'unadorned_announcement_bar_settings' );</code></pre>



<p class="wp-block-paragraph">Since there are no longer individual components for the fields and the <code>DataForm</code> uses an object for the <code>data</code> prop, it&#8217;s more straightforward to store the field state as an object too. This will also match what&#8217;s actually stored in the database.</p>



<p class="wp-block-paragraph">First replace the three separate state variables in <code>use-settings.js</code>:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const useSettings = () =&gt; {
    const [ settings, setSettings ] = useState( {
        message: '',
        display: false,
        size: 'small',
    } );

    // ...

    return [ settings, setSettings, saveSettings ];
};</code></pre>



<p class="wp-block-paragraph">Since the data stored in the options table matches the state structure exactly, you can simplify both reading and saving.</p>



<p class="wp-block-paragraph">For the initial data loading, update the success handler inside the <code>useEffect</code> hook:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const useSettings = () =&gt; {
    // ...

    useEffect( () =&gt; {
        apiFetch( { path: '/wp/v2/settings' } ).then( ( wpSettings ) =&gt; {
            setSettings( wpSettings.unadorned_announcement_bar )
        } );
    }, [] );

    // ...
};</code></pre>



<p class="wp-block-paragraph">For saving the settings, update the <code>saveSettings</code> as follows:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const useSettings = () =&gt; {
    // ...

    const saveSettings = () =&gt; {
        apiFetch( {
            path: '/wp/v2/settings',
            method: 'POST',
            data: {
                unadorned_announcement_bar: settings
            },
        } ).then( () =&gt; {
            // ...
        } );
    };

    // ...
};</code></pre>



<p class="wp-block-paragraph">Putting it all together, here&#8217;s how the <code>useSettings</code> should look after the previous updates:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const useSettings = () =&gt; {
    const [settings, setSettings] = useState({
        message: "",
        display: false,
        size: "small",
    });

    const { createSuccessNotice } = useDispatch(noticesStore);

    useEffect(() =&gt; {
        apiFetch({ path: "/wp/v2/settings" }).then((wpSettings) =&gt; {
            setSettings(wpSettings.unadorned_announcement_bar);
        });
    }, []);

    const saveSettings = () =&gt; {
        apiFetch({
            path: "/wp/v2/settings",
            method: "POST",
            data: {
                unadorned_announcement_bar: settings,
            },
        }).then(() =&gt; {
            createSuccessNotice(
                __("Settings saved.", "unadorned-announcement-bar"),
            );
        });
    };

    return {
        settings,
        setSettings,
        saveSettings,
    };
};</code></pre>



<h3 class="wp-block-heading" id="connecting-the-usesettings-with-dataform">Connecting the <code>useSettings</code> with <code>DataForm</code></h3>



<p class="wp-block-paragraph">Now that <code>useSettings</code> returns the state as a single object, update the <code>SettingsPage</code> component.</p>



<p class="wp-block-paragraph">Change how you destructure the hook, remove the <code>data</code> variable, and pass <code>settings</code> to <code>DataForm</code>.</p>



<p class="wp-block-paragraph">After the changes, the code in <code>/src/components/settings-page.jsx</code> should look like this:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    const [ settings, setSettings, saveSettings ] = useSettings();
    
    const fields = [
        // ...
    ]
    const form = {
        // ..
    }

    return (
        &lt;&gt;
            &lt;SettingsTitle /&gt;
            &lt;Notices /&gt;
            &lt;DataForm
                data={ settings }
                fields={ fields }
                form={ form }
                onChange={ () =&gt; {} }
            /&gt;
            &lt;SaveButton onClick={ saveSettings } /&gt;
        &lt;/&gt;
    );
};</code></pre>



<h3 class="wp-block-heading" id="implementing-the-onchange-callback">Implementing the <code>onChange</code> callback</h3>



<p class="wp-block-paragraph">The last part is updating the internal state (<code>settings</code>) whenever a field is updated. For this, you have to implement the <code>onChange</code> callback.</p>



<p class="wp-block-paragraph">The <code>onChange</code> callback only receives the changed data (the &#8220;edits&#8221;), not the complete state. For example, when you update the message field, <code>onChange</code> will receive <code>{ message: 'updated value' }</code>.</p>



<p class="wp-block-paragraph">This means you can&#8217;t simply pass the changes to <code>setSettings</code>, as it would replace the entire state with just the changed field. Instead, you have to merge the current state with the changes.</p>



<p class="wp-block-paragraph">Here&#8217;s how the <code>onChange</code> callback should look after the update:</p>



<pre class="wp-block-code"><code class="language-javascript" lang="javascript">const SettingsPage = () =&gt; {
    // ...

    return (
        &lt;&gt;
            &lt;SettingsTitle /&gt;
            &lt;Notices /&gt;
            &lt;DataForm
                data={ settings }
                fields={ fields }
                form={ form }
                onChange={ ( edits ) =&gt;
                    setSettings( ( current ) =&gt; ( {
                        ...current,
                        ...edits,
                    } ) )
                }
            /&gt;
            &lt;SaveButton onClick={ saveSettings } /&gt;
        &lt;/&gt;
    );
};</code></pre>



<p class="wp-block-paragraph">Essentially, the spread operator (<code>...</code>) first copies all properties from the <code>current</code> state, then overwrites any properties that exist in <code>edits</code>. This ensures unchanged fields keep their values while changed fields get updated.</p>



<p class="wp-block-paragraph">And with this, <strong>you successfully refactored the settings page</strong> using the <code>DataForm</code> component and configuration driven approach!</p>



<h2 class="wp-block-heading" id="wrapping-up">Wrapping up</h2>



<h3 class="wp-block-heading" id="try-it-yourself">Try it yourself</h3>



<p class="wp-block-paragraph">You can check the final result in the GitHub repository to see the <a href="https://github.com/wptrainingteam/unadorned-announcement-bar/tree/dataform-refactor">entire code together</a>, or you can <a href="https://github.com/wptrainingteam/unadorned-announcement-bar/compare/main...dataform-refactor">compare the two solutions</a>.</p>



<p class="wp-block-paragraph">If you want to try it out without downloading and installing it, you can do that <a href="https://playground.wordpress.net/#%7B%22landingPage%22:%22/wp-admin/admin.php?page=unadorned-announcement-bar%22,%22preferredVersions%22:%7B%22php%22:%228.3%22,%22wp%22:%226.9%22%7D,%22login%22:true,%22steps%22:[%7B%22step%22:%22installPlugin%22,%22pluginData%22:%7B%22resource%22:%22url%22,%22url%22:%22https://raw.githubusercontent.com/wptrainingteam/unadorned-announcement-bar/dataform-refactor/playground/release/2.0.0.zip%22%7D,%22options%22:%7B%22activate%22:true%7D%7D]%7D">using WordPress Playground</a>.</p>



<h3 class="wp-block-heading" id="where-to-go-from-here">Where to go from here</h3>



<p class="wp-block-paragraph">If you&#8217;re excited about <code>DataForm</code>, there are some other areas you can explore on your own.</p>



<p class="wp-block-paragraph">For example, you can look into the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/#validity">validation</a> feature that allows you to do client-side validation and define which fields are required, among other things.</p>



<p class="wp-block-paragraph">You can also look into how to <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/#getelements">load the <code>elements</code> asynchronously</a> instead of having them hardcoded. This would allow you to dynamically load the options of select fields from the database.</p>



<p class="wp-block-paragraph">It&#8217;s worth checking the <a href="https://wordpress.github.io/gutenberg/?path=/docs/dataviews-dataform--docs">Storybook</a> for the <code>DataForm</code> component, as it has interactive demos for all the layout types in various combinations.</p>



<p class="wp-block-paragraph">Lastly, to get up to speed with the latest changes the <a href="https://make.wordpress.org/core/2025/11/11/dataviews-dataform-et-al-in-wordpress-6-9/">DataViews, DataForm, et al. in WordPress 6.9</a> is a good starting point. For specific details, check the <a href="https://developer.wordpress.org/block-editor/reference-guides/packages/packages-dataviews/">package documentation page</a>.</p>



<p class="has-text-align-right wp-block-paragraph"><em>Props to <a href="https://profiles.wordpress.org/psykro/">@psykro</a> and <a href="https://profiles.wordpress.org/areziaal/">@areziaal</a> for their reviews, and to <a href="https://profiles.wordpress.org/juanmaguitar/">@juanmaguitar</a> for ongoing education about this topic.</em></p>



<p class="wp-block-paragraph"></p>

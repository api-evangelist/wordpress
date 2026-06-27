---
title: "Dynamically loading template parts in block themes"
url: "https://developer.wordpress.org/news/2026/06/dynamically-loading-template-parts-in-block-themes/"
date: "2026-06-18"
author: "Justin Tadlock"
feed_url: "https://developer.wordpress.org/news/feed/"
---
This tutorial shows how to avoid duplicating block theme templates by using the render_block_data filter to dynamically swap template parts based on context like post category or page type. A music project example displays different sidebars per category by modifying a template part's slug on the fly, using get_block_theme_folders() to locate parts and providing automatic fallback when no specific match exists. The approach works for any template part, including headers, footers, and banners.

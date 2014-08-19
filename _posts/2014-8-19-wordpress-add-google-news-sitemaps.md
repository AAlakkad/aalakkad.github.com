---
layout: post
title: "WordPress: Add Google News Sitemaps using WordPress SEO"
description: ""
---

## Introduction

In this article, you're going to learn how to add [Google News](https://news.google.com/) Sitemaps to your WordPress site without installing any additional plugin when you already have [WordPress SEO](https://yoast.com/wordpress/plugins/seo/).

Google News require special kind of sitemaps in order to crawl it as **News**, Webmasters Tools sitemaps will NOT work for **Google News**.

## Pre-requests

Acually you can implement the code without any pre-requests other than [WordPress SEO](https://yoast.com/wordpress/plugins/seo/) plugin, but the site owner should be listed in Google News so it make use of the News sitemap.


## The Code

Let's assume we're going to implement the News sitemap inside a theme, you can do it in any plugin too.


First we use the global WPSEO_Sitemaps class to register our custom sitemap using `register_sitemap` function.

`register_sitemap` function accept 3 parameters:

- `$name` of the sitemap
- `$function` callback to build the sitemap
- `$rewrite` Regex to match the sitemap e.g. the sitemap public URL.

To start, put this inside your theme `functions.php` file:

```php
<?php
if(class_exists('WPSEO_Sitemaps')) {
    add_action('init', 'my_custom_google_news_sitemap');
    
    function my_custom_google_news_sitemap() {
        $GLOBALS['wpseo_sitemaps']->register_sitemap( 'google-news-sitemap', function() {}, 'sitemap_news.xml' );
    }
}
```

Now we've a basic custom sitemap ready to be populated with proper data.

Note: if you get a 404 error, you may want to `flush_rewrite_rules()`,  or go to Settings -> Permalink and just click save.

### Populate Data

This time you should use `get_posts` rather that `WP_Query` class, for some reason it won't work!

Inside custom sitemap callback function: 

```php
<?php
$query_args = [
     'post_type' => 'post',
     'post_status' => 'publish',
     'posts_per_page' => 1000, // Google bots won't crawl more than 1000 entries per sitemap
     'paged' => 1
];
$posts = get_posts($query_args);

```

The next step is to append query result to an XML content, we'll continue after `get_posts` statement and some explanation will be inside code.

```php
<?php
$xml = '<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:news="http://www.google.com/schemas/sitemap-news/0.9">';
foreach($posts as $post) {
    $permalink = get_permalink($post->ID);

    $title = $post->post_title;
    $site_title = get_bloginfo( 'name' ); // get site's name
    $language = get_bloginfo( 'language' ); // get site's language (e.g. en or ar)
    $date = get_the_time( 'c', $post->ID ); // c is the complete date plus hours, minutes, seconds and a decimal fraction of a second which is accepted by Google
    $genres = 'PressRelease'; // Comma-seperated geners
    $keywords = 'comma, seperated, keywords'; // Comma-seperated keywords

    $xml .= <<<XML
          <url>
            <loc>{$permalink}</loc>
            <news:news>
              <news:publication>
                <news:name>{$site_title}</news:name>
                <news:language>{$language}</news:language>
              </news:publication>
              <news:genres>{$genres}</news:genres>
              <news:publication_date>{$date}</news:publication_date>
              <news:title>{$title}</news:title>
              <news:keywords>{$keywords}</news:keywords>
            </news:news>
          </url>
XML;
}
$xml .= '</urlset>';

echo $xml;

// Remove any wp_footer actions and die()
$GLOBALS['wpseo_sitemaps']->sitemap_close();
```

To get the full genres list check [Google Help center](https://support.google.com/news/publisher/answer/93992 "Content types").

Remember to replace the comma-seperated keywords with real keywords, you can use tags or categories.

## Conclusion

As you saw, it's easy to implement Google News Sitemaps without installing another plugin when you have WordPress SEO.

[WordPress SEO](https://yoast.com/wordpress/plugins/seo/) has a [paid plugin](https://yoast.com/wordpress/plugins/news-seo/) designed for Google News, check it out.


You can find the complete code we wrote [here](https://gist.github.com/AAlakkad/c28afd0a4068f23d5ee1) on Github Gist.

--- 

Finally, I would like to thank [Louy](https://github.com/louy) for the advice about using the custom sitemaps with WordPress SEO!
---
layout: post
title: "Add rules to WordPress robots.txt"
excerpt: "Addig rules to virtual robots.txt in WordPress"
---

There's 2 types of robots.txt files in WordPress, it's either virtual (generated by WordPress on requests) or real existing file.

To add rules to the virtual robots.txt file you need to *hook* into `robots_txt` filter, like this: 

```php
<?php
add_filter('robots_txt', function($content, $is_public) {
    $content .= "\n";
    $content .= "User-Agent: *";
    $content .= "\n";
    $content .= "Allow: /";
    return $content;
}, 10, 2);
```

The `robots_txt` filter accepts 2 parameters:

- `$content`: is the content of robots.txt file to be displayed.
- `$is_public`: whether the WordPress settings disallow search engines from accessing the website.

In the function above we're appending rules to the already existing content and returning it. not overriding it.
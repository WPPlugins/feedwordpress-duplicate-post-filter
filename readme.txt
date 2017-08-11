=== FeedWordPress Duplicate Post Filter  ===
Contributors: mrallen1
Tags: duplicate posts, feedwordpress
Requires at least: 2.8
Tested up to: 3.3.1
Stable tag: 1.5

A FeedWordPress syndicated post filter that checks for duplicates before posting items from your feeds.

== Description ==
This is a filter for the FeedWordPress plugin. **If you don't use FeedWordPress this plugin will not be useful to you.**

I wrote this filter after seeing the same post in my database 32 times.  Maybe you've had the same problem, and I hope this filter helps you solve it.

The filter works by hooking the "syndicated_post" action of FeedWordPress and the "save_post" action in the core of WordPress.

For each potential post from a feed, the plugin attempts to find an identical SHA1 hash of the first 1024 non-whitespace characters (stripped of HTML tags) of the post content. 
If it finds a match the post is skipped. If not, the post is processed and a hash is inserted into the post's metadata. (Stored as key _dpf.)

**NOTE:** No filter is going to be 100% accurate.  This filter will stop *most* or *some* duplicates, but in all likelihood, will not stop *all* of them.
If you want a filter that stops *all* duplicates, this isn't your solution. In my test installation I had 5 posted duplicates out of 
125 syndicated posts (4% false negative) out of a corpus of about 300 duplicates. Most of those false negatives were due to slightly different HTML markup 
in the post content itself. So my approach isn't perfect, but it is "good enough" for me.

== Installation ==
1. Download the plugin and uncompress it.
2. Plop it in the same directory as feedwordpress.php
3. Enable this filter in WordPress by visiting the "Plugin" menu and activating it.

== Important Note ==
This filter can only check future syndication posts.  Whatever duplicates are already present in your WordPress installation you'll have to remove/clean-up on your own.

== Changelog ==
1.5 - Remove HTML tags before computing hash.

1.4 - Overhauled strategy for duplicate detection. This works better than previous strategies.

1.3 - Fixed a dumb typo. Rewrote the DB query using better wpdb methods (prepare and query). Changed from htmlescape2 to esc_html WP function.

1.2 - Escaping the single quote (') character sometimes gives a conversion of &amp;#8217; instead of &#8217; This caused a false negative and duplicate posts would be stored. Consider this release a temporary hack until I write a proper regex based title escape function.

1.1 - Characters in post-titles like '&' were not getting converted to HTML entities. This caused the post title comparison to register a false negative. (So duplicate posts would be added to your feed.)

1.0 - initial release

== License ==
Copyright (C) 2012 by Mark R. Allen
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
* Neither the name of Mark Allen nor the names of any contributors may be used to endorse or promote products derived from this software without specific prior written permission.

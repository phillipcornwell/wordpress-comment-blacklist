# Comment Blacklist for WordPress

#### Sometimes simple is better.

Over the past couple of years, I have identified over 11,000 phrases, patterns, and keywords commonly used by spammers and comment bots in usernames, email addresses, link text, and URIs. This blacklist is an ongoing work in progress and as such, there is always room for optimization and improvement. Suggestions and bug reports are certainly appreciated. Please use the [issue tracker](https://github.com/splorp/wordpress-comment-blacklist/issues) to let me know.

## How Do I Use It?

#### Manual Installation

Copy the list of keywords found in the [blacklist.txt](https://raw.github.com/splorp/wordpress-comment-blacklist/master/blacklist.txt) file, paste it into the [Comment Blacklist](http://codex.wordpress.org/Combating_Comment_Spam#Comment_Blacklist) field of your WordPress [Discussion Settings](http://codex.wordpress.org/Settings_Discussion_Screen) panel, and click the “Save Changes” button.

That’s it.

Repeat this procedure each time you want to install an updated version of the blacklist.

#### Automatic Updates Via Plugin

If you prefer a more hands-off approach, there are several plugins that will check whether the [master blacklist](https://raw.github.com/splorp/wordpress-comment-blacklist/master/blacklist.txt) has changed and then automatically install the most recent version. How handy is that?

+ [Blacklist Auto Updater](https://github.com/sergejmueller/wp-blacklist-updater) by [Sergej Müller](https://github.com/sergejmueller)
+ [Comment Blacklist Manager](http://wordpress.org/plugins/comment-blacklist-manager/) by [Andrew Norcross](https://github.com/norcross) 
+ [WordPress Simple Firewall](http://wordpress.org/plugins/wp-simple-firewall/) by [iControlWP](http://www.icontrolwp.com/)

## Does It Really Work?

I don’t blame you if you’re skeptical about how well this blacklist works compared to a commercial solution like [Akismet](http://akismet.com/). Because I am subjectively including keywords based on comment spam submitted to my own sites, there is a chance that the blacklist will “overclean” your comment queue. Consider that fair warning.

However, [Jason Cosper](https://github.com/boogah) reports that he used an earlier version of the blacklist on a client’s WordPress installation containing 800,000 or so comments. The blacklist flagged 40% of those comments as “spammy”. As a sanity check, he then exported those flagged comments to a local WordPress install and subsequently had Akismet do its thing. According to Jason, there were [“zero false positives.”](https://twitter.com/boogah/status/292031513590128640)

Still need convincing? The blacklist was featured over at [WP Daily](http://torquemag.io/torque-and-the-wp-daily-archives/) (now [Torque](http://torquemag.io/) in [John Saddington](http://john.do/)’s enticingly titled post, [Die Spam! Blacklist That Shiz with This Gist!](http://torquemag.io/comment-blacklist-gist/)

## Technical Considerations

WordPress stores the contents of the [Comment Blacklist](http://codex.wordpress.org/Combating_Comment_Spam#Comment_Blacklist) setting in a MySQL column named `blacklist_keys`. Defined as a `longtext` [data type](http://dev.mysql.com/doc/en/blob.html), this column can contain up to 4,294,967,295 bytes (approximately 4GB) of text. There is no chance of us running out of room to expand the blacklist any time soon.

## Known Issues

**URL Shorteners**

As mentioned above, the keywords in the blacklist are based on spam submitted to my own sites. Spammers often utilize the obscuring capabilities of URL shorteners to hide their nefarious links. Therefore, I have included a handful of URL shortener domains in the blacklist. For all practical purposes, there’s no need for a comment to include a shortened URL, as unmodified links can be easily formatted using HTML. You may want to remove the following keywords from the blacklist if you find that your visitors are using shortened URLs on a regular basis.

+ 2u4.us
+ 4ft.me
+ an0n.me
+ ano.gd
+ ateffa.ms
+ b54.in
+ bit.ly
+ cek.li
+ clck.ru
+ cort.as
+ fc.cx
+ goo.gl
+ hfg.cc
+ is.gd
+ loorg.de
+ smsh.me
+ snipurl.com
+ stan.to
+ tiny.cc
+ tinyurl.com
+ tr.im
+ urlms.com

**WordPress Links**

Spammers will also utilize links that include URLs that are specific to WordPress installations. These links often point at compromised admin, theme, or plugin files. In most cases, there’s no need to include a URL that deep-links into the bowels of a WordPress site. However, you may want to remove the following keywords from the blacklist if your visitors are commenting on topics related to WordPress site, plugin, or theme development.

+ /wp-admin
+ /wp-content
+ /wp-image
+ /wp-include
+ /wp-list
+ /wp-site

**Non-English Comments**

This blacklist has been created for use on English language sites. There are several dozen terms and phrases included in the blacklist that may flag legitimate comments posted in other languages. If you commonly receive comments in other languages (specifically those containing CJK, Hiragana, Katakana, Thai, or Cyrillic characters), you may want to remove or modify those sections of the blacklist.

**HTML Tag Attributes**

The blacklist is not applied against HTML tag attributes found in comments, only the values assigned to those attributes. This means that you cannot include the attribute name, equal sign, or the quote marks as part a keyword. For example, the keyword phrase `title="Discount` will not match anything, even if that exact bit of text exists within the content of an HTML formatted comment. A keyword consisting of `Discount` should be used instead. Other HTML attributes commonly allowed in WordPress comments such as `href=""`, `cite=""`, and `datetime=""` are also ignored.

**User Agent Strings**

According to the WordPress [Discussion Settings Screen](http://codex.wordpress.org/Settings_Discussion_Screen) documentation, a comment will be marked spam if any of the [Comment Blacklist](http://codex.wordpress.org/Combating_Comment_Spam#Comment_Blacklist) keywords are found in the comment content, name, URL, email, or IP address fields. Surprisingly, WordPress also applies the blacklist against the [user agent](http://en.wikipedia.org/wiki/User_agent) string.

For example, in an earlier version of the blacklist the keywords `/4.` and `/5.` had been included to flag URLs with sequentially numbered pages with various file extensions. Unfortunately, these two benign-looking keywords also flagged comments containing common user agent strings, such as `Mozilla/4.0` and `Chrome/5.0`. In other words, nearly every single comment was flagged as spam, regardless of its content or whether the commenter had been previously approved.

## Mad Props

*“So much for using Akismet.”*

Thanks to [Mika Epstein](https://github.com/ipstenu), [Paul Goodchild](https://twitter.com/PaulGoodchild), [Sergej Müller](https://github.com/sergejmueller), [Andrew Norcross](https://github.com/norcross), [Claudio Schwarz](https://github.com/purzlbaum), and [Volker Schmidt](https://github.com/volkerjschmidt) for their various contributions, suggestions, and reports from the field.

Finally, [Chris Burton](https://twitter.com/chrisburton/status/431581759277633536) deserves a virtual fist bump for the above tweet.

## License

Copyright © 2011–2014 Grant Hutchinson

This project is licensed under the short and sweet [MIT License](http://opensource.org/licenses/MIT). This license allows you to do anything pretty much anything you want with the contents of the repository, as long as you provide proper attribution and don’t hold anyone liable.

See the [license.txt](https://raw.github.com/splorp/wordpress-comment-blacklist/master/license.txt) file included in this repository for further details.

## History

+ 20140624 — 11,000 entries
+ 20140527 — [WordPress Simple Firewall](http://wordpress.org/plugins/wp-simple-firewall/) plugin adds “human spam comment filtering” support
+ 20140527 — Added [MIT License](http://opensource.org/licenses/MIT)
+ 20140501 — Andrew Norcross’s [Comment Blacklist Manager](https://github.com/sergejmueller/wp-blacklist-updater) plugin released
+ 20140501 — Sergej Müller’s [Blacklist Auto Updater](https://github.com/sergejmueller/wp-blacklist-updater) plugin released
+ 20140508 — 10,000 entries
+ 20140324 — 9,000 entries
+ 20140130 - Mentioned on [Narga](http://www.narga.net/stop-wordpress-spam-comments-trackbracks/)
+ 20130206 — 8,000 entries
+ 20131215 — 7,000 entries
+ 20131105 — Migrated project to [GitHub](https://github.com/splorp/wordpress-comment-blacklist)
+ 20131020 — 6,000 entries
+ 20130911 — 5,000 entries
+ 20130715 — 4,000 entries
+ 20130226 — 3,000 entries
+ 20130130 — Added documentation
+ 20130130 — Mentioned on [WP Daily](http://torquemag.io/comment-blacklist-gist/)
+ 20120529 — 2,000 entries
+ 20120217 — 1,000 entries
+ 20111122 — Released as a [Gist](https://gist.github.com/splorp/1385930) with just over 140 entries


## Questions?

Contact me on Twitter.

[@splorp](https://twitter.com/splorp)

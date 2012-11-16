# OpenBook

A protocol over HTTPS and utilizing JSON and Markdown to share content and send feedback. Learn more on the [official OpenBook site](https://projectopencontent.org/OpenBook.html). Also stay up to date at [projectopencontent.org](https://projectopencontent.org/).

This protocol is a just the start of a draft, so join in and start contributing, or check back soon to see our rapid progress. :-D

### What is OpenBook

OpenBook is an open protocol to share content with your friends, like HTTP or email, except with enhanced social features. Users can create their own host and make up their own rules, but most users will use a large provider who has gained some popularity. 

Some providers will allow complete control, while others will gain large userbases because they keep policies simple. All providers and users will have full control over their content on OpenBook. Just like the web, if you know the url and it is publicly available, you can get it. 

## Peers

The following are all examples of peers in an OpenBook network:

* `username.friendbook.com` - the super-peer, or provider, is `friendbook.com`
* `first.last.name` - while `last.name` could be the provider, it is not in this case
* `myblog.org`

A peer is located at any (sub)domain. For example, a provider may provide their service at friendbook.com. A user might create an account with that provider, and the provider might offer an account for the user at username.friendbook.com. This is the user's OpenBook address.


## Pages

A page is a single piece of content provided by an OpenBook host. Each page is addressed by a url just like HTTP. 

A page has a title, rich content (including links and OpenBook links), and an 'origionally posted' timestamp. The owner/publisher is the simply the peer who publishes the page.

Peers can decide when to publish and stop publishing a page.

# Getting Started

To learn how to get start connecting to OpenBook, head on over to the start of the [protocol document](Protocol.md)

# License

Released under the Apache 2 License. You are free to use OpenBook however you'd like. If make changes to OpenBook and distribute them, you must call the project something else to avoid confusion with this one.

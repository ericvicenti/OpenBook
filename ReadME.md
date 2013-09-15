# OpenBook

A protocol over HTTPS and utilizing JSON and Markdown to share content and send feedback. Learn more on the [official OpenBook site](https://projectopencontent.org/OpenBook.html). Also stay up to date at [projectopencontent.org](https://projectopencontent.org/).

### What is OpenBook

OpenBook is an open protocol to share content with your friends, like HTTP or email, except with enhanced social features. Users can create their own host and make up their own rules, but most users will use a large provider who has gained some popularity. 

Some providers will allow complete control, while others will gain large userbases because they keep policies simple. All providers and users will have full control over their content on OpenBook. Just like the web, if you know the url and it is publicly available, you can get it. 

## Peers

The following are all examples of peers in an OpenBook network:

* `username.friendbook.com` - the super-peer might be `friendbook.com`
* `first.last.name` - the super-peer might be `last.name`
* `myblog.org`

A peer is located at any (sub)domain. For example, a provider may provide their service at friendbook.com. A user might create an account with that provider, and the provider might offer an account for the user at username.friendbook.com. This is the user's OpenBook address.

Each peer is also a server. When describing requests, the peer recieving the request is considered the server.

## Pages

A page is a single piece of content provided by an OpenBook peer. Each page is addressed by a normal url.

Each peer is expected to have an index page of some sort available at '/'.

Pages have a title, a [simpleMarkdown](SimpleMarkdown.md) body (including links and OpenBook links), contextual links, and a 'last updated' timestamp. The publisher of the content is the simply the peer who serves the page.

Publishers have immense flexibility when publishing a page. A peer can decide who to publish a page for. Perhaps the peer only serves the content for a particular group of peers, or maybe the publisher does not want to send the page to certian peers. Or, the publisher could send a modified version of the page when certian peers request it.

## Protocol

OpenBook peers make requests with eachother following these rules: [OpenBook Requests](Requests.md).

These are the two actions peers use to connect and share:

- [GET: Get a peer's published content](Getting.md)

- [POST: Send content links or feedback to a peer](Posting.md)

# License

[Released under the MIT License](LICENSE.md).

You are free to use OpenBook protocol however you'd like.

If make changes to the OpenBook protocol and distribute them, you must call the project something else to avoid confusion with OpenBook.

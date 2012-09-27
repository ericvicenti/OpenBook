# OpenBook

A protocol over HTTP and utilizing SSL to share content and send feedback.

This is on GitHub because this should be a collaborative process. If you have ideas, improvements, or comments, feel free to make issues and pull requests.

### What is OpenBook

OpenBook is an open protocol to share content with your friends, like HTTP or email, except with enhanced social features. Users can create their own host and make up their own rules, but most users will use a large provider who has gained some popularity. 

Some providers will allow complete control, while others will gain large userbases because they keep policies simple. All providers and users will have full access to all content on OpenBook. Just like the web, if you know the url and it is publicly available, you can see it. But now, you have a powerful way of identifying your friends and enemies.

OpenBook if a very, very flexible protocol. You are not pidgeon-holed into a simple social design like twitter. OpenBook defines only the broadest characteristics that all social networks share.

### What OpenBook Defines

* How to browse content. Content can contain rich text and links, and can be structured in a heirechal fashion using traditional paths

* A specific content format

* A method to authenticate users and providers with each-other

  * In order to treat feedback and responses from that host specially

  * In order to recognize content that comes from the same place
  
  * In order to know when a host is managed by a super-host

* A method for responses to be sent to a page across hosts

* A method for positive/negitive feedback to be provided to a page about the OpenBook content it contains

### What the Providers & Users Define

* The way OpenBook content is displayed to the user

* Features like 'friends' or 'saved content' which are both fancy ways of saving URLs or downloading another server's content

* A provider can interface with it's users in any way it chooses, although providers will commonly implement web front-ends for their users

* Providers should vary in content policies:
  
  * can be very reddit-like and will allow everyone to vote on content and contribute
  
  * could force public editability of pages while supporting a version history, like wikipedia
  
  * might not accept public feedback, acting like a blog / publishing platform / cms

* Determining security settings: by whitelisting or blacklisting domains, and recognizing hosts with good behavior
  * Hosts can behave differently to other hosts or super-hosts which it recognizes
  * Ability to submit feedback, submit pages, or access content should vary from host to host

## Hosts
The following are all examples of hosts in an OpenBook network:

* `username.friendbook.com` - the super-host, or provider here, is `friendbook.com`
* `first.last.name` - while `last.name` could be the provider, it is not in this case
* `myblog.org`
An OpenBook host represents one specific point of trust, and is often a user. ie.  or  or . This is important because the behavior of `username.friendbook.com` might be widely dependent on friendbook's policies, so it important to know what patterns that entity will follow. It allows providers to build trust amongst eachother and whitelist eachother to build a stronger network amidst the internet space-junk. It allows some systems to be built which follow strict rules, while competing systems can be built which offer alternate behavior, all of which will be entirely displayble and viewable by every OpenBook client.

While one server can typically handle thousands of hosts, a server can also be configured to handle only one host. One host can be also served from many servers in the rare cases when that would be necessesary (like for celebrities or political leaders)

A server is located at any subdomain. For example, a provider may provide their service at friendbook.com. A user might create an account with that provider, and the provider might offer an account for the user at username.friendbook.com. This is the user's OpenBook address.

## Providers

A provider is a super-host. In order to be a provider, you must own the parent domain which hosts reside under. In our example, the user is `username.friendbook.com`, and the provider is `friendbook.com`. A provider is expected to have its own set of behaviors and policies. It will choose to interact with other providers and hosts if they behave well, or if there is some recognition or external validation.

The flexibility of OpenBook allows for an intricate ecosystem of providers, with the ability to delegate policy-making indefinitely.

## Pages

A page is a single piece of content provided by an OpenBook host. Each page is addressed by a url just like HTTP. 

A page has a title, rich content (including links and OpenBook links), and an 'origionally posted' timestamp. The owner/publisher is the host where the page is found on.

Hosts decide when to publish and stop publishing a page.

A page must accept responses and positive/negative feedback to whatever responses it currently links to.
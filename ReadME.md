# OpenBook

A protocol over HTTP and utilizing SSL to share content and send feedback.

Speaking of feedback, this project is of course a major work in progress. I refuse to put a version number on it until it gets a little further. I need your help and I welcome contributions, feedback, comments, and insults.

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
  
  * could force public editability of posts while supporting a version history, like wikipedia
  
  * might not accept public feedback, acting like a blog / publishing platform / cms

* Determining security settings: by whitelisting or blacklisting domains, and recognizing hosts with good behavior
  * Hosts can behave differently to other hosts or super-hosts which it recognizes
  * Ability to submit feedback, submit posts, or access content should vary from host to host

## Hosts (OpenBook Users)

An OpenBook host represents one specific point of trust, and is often a user. ie. `username.friendbook.com` or `first.last.name` or `myblog.org`. This is important because the behavior of `username.friendbook.com` might be widely dependent on friendbook's policies, so it important to know what patterns that entity will follow. It allows providers to build trust amongst eachother and whitelist eachother to build a stronger network amidst the internet space-junk. It allows some systems to be built which follow strict rules, while competing systems can be built which offer alternate behavior, all of which will be entirely displayble and viewable by every OpenBook client.

While one server can typically handle thousands of hosts, a server can also be configured to handle only one host. One host can be also served from many servers in the rare cases when that would be necessesary (like for celebrities or political leaders)

A server is located at any subdomain. For example, a provider may provide their service at friendbook.com. A user might create an account with that provider, and the provider might offer an account for the user at username.friendbook.com. This is the user's OpenBook address.

## Providers

A provider is a super-host. In order to be a provider, you must own the parent domain which hosts reside under. In our example, the user is `username.friendbook.com`, and the provider is `friendbook.com`. Because it might be expensive to assign a different SSL key for every friendbook user, sub-hosts can delegate their networking duties to their parent.

## Posts

A post is the name for a bit of OpenBook content. They reside under any path under the host. For example, a blog post might be located at `http://first.last.name/blog/2012/hello_world`. A post can reside at _any valid url_ under the host. 

ONE post is required per Host, which must be located at the host root (path /). This will most commonly be a list of all of the user's public posts.

A post contains the following:

* Title
 
* Time Posted

* Content (can contain rich text, OpenBook links, and normal links)


## Post Retrieval
A post is a container of info, provided in a specific format from an openbook server. An openbook server determines its own post addresses. When a post is requested from an openbook server over HTTPS via a GET, the server should respond with the following:

* "title": String

  The title of the post, limited to 140 characters, which should not contain links or anything other than Unicode text


* "body": String

  The URL where the content of the post can be found.


* "date": Integer

  A UNIX timestamp of the first posting of this content


* "policy": String

  The organization's given name for the policy by which this post is governed.

## Server Authentication

Authentication is entirely optional, all requests are valid in HTTP or HTTPS. Most often, only public content will be available from HTTP GET, and all other verbs on HTTP, as well as all restricted content, will use a redirect to point to an HTTPS resource, or will return a 403 Forbidden.

### Example

A host makes an initial request to another; `somebody.name` is trying to recieve content from another host, `username.friendbook.com`. `somebody.name` provides an HTTP header which identifies itself as `somebody.name`. Now `username.friendbook.com`, who does not recognize the public key being used by the requester, needs to verify that this server is the real authority for `somebody.name`.


`username.friendbook.com` requests a host identity check on `somebody.name`. It connects over HTTPS using typical SSL security chains to trust them up until this point. `somebody.name` responds with a public key, which is saved as a known host, and is matched up against the public key being used to connect.

At this point `username.friendbook.com` can trust that they are truly talking to `somebody.name`. Based on the trust involved in dns inheritance, friendbook can decide if `somebody.name` has access. Because he is just getting content, friendbook allows it.

### Host Identity Check

A host queries another host's for it's basic information by making a HTTPS GET request to `https://HOST_NAME/_auth`

The auth response contains the following:

* "key": String

  The public SSL key that this host uses to authenticate with


## Page Submission

A link to a page can be sent from one server to another. For example, `somebody.name` wants to post some content to her friend's page at `username.friendbook.com`. If friendbook implicitly trusts 'somebody.name', the content might instantly appear on the page. Friendbook might also only recognize and allow content from other providers, like `gbook.com`.

If a server is authenticated to another, it can always submit a page. What the recieving host does with the OpenBook link is up to it. For some providers it will be used as a feedback mechanism, a sort of in-line email response to content. Other providers will build heirechal discussion boards with this ability.

## Feedback Submission

Feedback is a mechanism by which a server can tell another server that what it links to is good or bad. This might be recognized as a 'like', 'upvote', or 'downvote'. In any case, it is up to the host to respond to the feedback. Most benevolent providers will force the displaying of feedback, and some (like ones which model reddit) will use the feedback to order content and push other content off the page or onto other pages. It is up to the provider to establish concepts like 'karma'.

For example, say a spammer posted a link to `username.friendbook.com` post. `somebody.name` wants to tell our friendbook server that the link posted by the spammer is bad.

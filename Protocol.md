# Protocol

This is on GitHub because this should be a collaborative process. If you have ideas, improvements, or comments, feel free to make issues and pull requests.

## Basics

### HTTP Consistencies

OpenBook builds upon the success and features of HTTP. For example, OpenBook supports encrypted and unencrypted access over ports 443 and 80, respectively. For initial https interactions, a typical SSL encryption chain is used.

OpenBook servers should send and respond to the following HTTP status codes:

* 200 - Success / Data
* 301 - Moved
* 302 - Forward
* 400 - Invalid Request
* 403 - Access not allowed
* 404 - Page not found
* 500 - Server Error

Forwards can happen across protocols. ie, if a host wants to demand HTTPS, they can forward from the HTTP to the HTTPS, which will trigger the typical SSL authenticaiton process. Forwards are also used for typical path manipulation within a host. Lastly, when a forward is made to another host, that host is should be authenticated normally.

OpenBook hosts need to support and supply only the following HTTP verbs:

* GET - For retrieving pages and authentication


### SSL Authentication

For most verbs and routes, hosts will demand encryption by redirecting to HTTPS. When a host connects to a peer


## Methods

### GET Authentication

A host knows it should respond with its authentication when you GET `host.name/_auth`

### GET Post

A host provides content when requested with a GET request. Hosts can server traditional HTML sites alongside OpenBook posts, if it chooses.

### PUT Post


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

# OpenBook

A protocol over HTTP & HTTPS to submit and publish content, share feedback, and take content contributions.

### What OpenBook Defines

* A method to browse OpenBook content

* Content formatting, so each client can choose how to display it

* A method to authenticate users with each-other

* A method for OpenBook responses to be sent to a page

* A method for positive/negitive feedback to be provided to a page about the OpenBook content it contains

### What the Provider Defines

* A user can interface with a provider in any way the provider chooses, although providers will commonly implement web front-ends

* Providers should vary in content policies:
  
  * can be very reddit-like and will allow everyone to vote on content and contribute
  
  * could force public editability of posts while supporting a version history, like wikipedia
  
  * might not accept public feedback, acting like a blog / publishing platform / cms

### Conventions

All of the basic requests will specify HTTP verb and method, as they change based on the type of the request. All requests transfer data with JSON, and the `Content-Type` should be labelled as such. The standard encoding for all of openbook, including paths and server addresses, is UTF-8, with full unicode character support.

## Hosts

An OpenBook host represents a user, and allows a user to be addressed by a domain name. ie. `username.friendbook.com` or `first.last.name`

While one server can typically handle thousands of hosts, a server can also be configured to handle only one host. One host can be also served from many servers in the rare cases when that would be necessesary (like for celebrities or political leaders)

A server is located at any subdomain. For example, a provider may provide their service at friendbook.com. A user might create an account with that provider, and the provider might offer an account for the user at username.friendbook.com. This is the user's OpenBook address.

## Providers

A provider represents a super-host of sorts.

## Posts

A post is the name for a bit of content in 


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

OpenBook servers authenticate with one another with OpenSSL key-pairs. 

### Auth Get

A host queries another host's for it's basic information by making a HTTPS GET request to `https://HOST_NAME/_auth`

The auth response contains the following:

* "key": String

  The public SSL key that this host uses to authenticate with


### Auth Post



## Page Submission

A link to a page can be sent from one server to another. For example, `somebody.name` wants to post some content to her friend's page at `username.friendbook.com`.

## Feedback Submission

Feedback is a mechanism by which a server can tell another server that what it links to is good or bad. For example, say a spammer posted a link to `username.friendbook.com` post. `somebody.name` wants to tell our friendbook server that the link posted by the spammer is bad.

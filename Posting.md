# Posting

Post Objects are lightweight messages exchanged between peers.

## Post Object

A post is a single action from a peer to a server. A Post Object sends links, conveys opinions, and requests notification for updates.

```
  {
    link: 'https://...',
    opinion: 'like',
    subscribe: 'https://...',
    target: 'https://...',
    peer: 'https://...'
  }
```

### Link

Link can be either a link which the server already refrences on the target page, or a new link that the peer would like to tell the server about. The link can be a normal web link, or a page on an OpenBook peer.

Any post object with a link is considered a "link post". Publishing and link-posting is the primary way of sending new content to a destination.

### Opinion

The "opinion" is a relationship between the peer and the specified `link`. If no link is specified in the post object, the opinion describes the post object target page.

`opinion` can be:

- "like" - The peer supports the content
- "dislike" - The peer dislikes the content
- "warn" - The content is offensive and against the claimed rules of the server
- null - Resets the peer's opinion of the content

If a post object has an opinion, it is considered an "opinion post".

### Subscription

A subscription is a peer's way of telling a server that it wants page updates & new sub-pages when the server has them.

The subscription link is the requested destination of update posts. The subscription link should always be a link on the peer who is sending. (ie, one peer should not be able to subscribe another peer for updates; only themselves)

A "subscription post" is any post with the `subscribe` attribute set. Subscription posts modify a subscription relationship between the peer and the target page. Because the terms do not overlap, it is possible to combine subscription posts with opinion or link posts.

To unsubscribe or modify a subscription, a peer should send a post object to the same target with `subscription` changed or set to an empty string.

### Peer

Peer is the sender of the post. Peer is optional because the server can securely identify the peer with host authentication.

The server should only accept an altered peer field if the real sender is a super-peer authorized to post on behalf of the named sub-peer.

### Target

The target page is the destination of the post object. Every post object has a target, but the target attribute itself is optional. If `target` is undefined or empty, the server can determine the target based on the url of the page which the peer is POSTing to.

The target attribute can modify the destination peer, and/or the destination path. For example, if a peer wants to send a link to two sub-peers at once, they can send a multi-post to the super-peer with different target URLs. Or, if a peer wants to send an opinion to two target pages on one server, they can send a multi-post with different opinion objects for each target.

## Post Responses

### Status Codes

* 200 - Successful post
* 400 - Bad post
* 401 - Bad authentication
* 500 - Unexpected server error

These codes will be sent as normal HTTP status codes for normal single-object posts, and will be included in the `status` attribute for multi-posts.

### Success Response

If the request is successful, the response will be the server's interpretation of the requested Post Object. If the peers are communicating perfectly, the object will be identical.

### Error Response

See [Openbook Errors](Errors.md).

## Types of POSTing

### Normal, Single Object Post

A single Post Object can be sent in a POST [OpenBook Request](Requests.md).

Responses will will be a normal JSON object, and should have an appropriate HTTP response code.

### Multi-Object Post

If the request body of an OpenBook POST is an array, the peer is sending multiple Post Objects at once.

#### Multi-Post Response Codes

HTTP response codes for Multi-Posts are as follows:

* 200 - Multi-Post successfully recieved, intrepreted and responded to
* 400 - Poorly formatted Multi-Object POST
* 500 - Server error responding to Multi-Object POST

#### Multi-Post Response

The successful (code 200) response body for a multi-post is an array of the following objects, corresponding to the array of send Post Objects. The `status` and response of these objects should match the status code and response of a normal Object Post.

```
  {
    status: INT,
    response: {...}
  }
```

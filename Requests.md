# OpenBook Requests

An OpenBook request is an HTTPS request with the header `OpenBookVersion` set.

## OpenBook Header

OpenBook requests have the header set as following:

  "OpenBookVersion": "0.1"

The version should be equal or greater to 0.1, as this is the first version.

## Host Authentication

OpenBook requests are [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure) requests. By using a normal SSL security chain, OpenBook peers can identify eachother.

For example, most peers will trust eachother using the standard set of top-level certificates that browsers use to securely identify web sites. If your server & certificate allows browsers to securely connect (and authenticate the host without any warnings), then other peers can also securely connect.

If a peer does not want to automatically trust everybody else, or if they do not want to purchase commercial SSL certificates, they can install custom certificates for their peers, and/or set up their own [certificate authority](http://en.wikipedia.org/wiki/Certificate_authority).

## Peer Header

Peer is the sender of the request. Thanks to host authentication, the requester is always identified as the 'authenticated peer'. The authenticated peer is used if the peer header is omitted.

Sometimes, a different peer must be specified. For example, a super-peer might want to request a page for a sub-peer.

  "OpenBookPeer": "myname.openface.com"

Peer headers must be validated to ensure the authenticated peer is allowed to act as the peer they specify. For example, `openface.com` can act as `myname.openface.com` but not as `facebook.com`. OpenBook peers need to verify this in order to prevent spoofing.

## Methods

Openbook supports the following HTTP methods on pages:

- [GET (publishing)](Getting.md)
- [POST (contributing)](Posting.md)
# Getting Started

This is on GitHub because this should be a collaborative process. If you have ideas, improvements, or comments, feel free to make issues and pull requests.

## Basics

An OpenBook request is an HTTPS request with the header `OpenBookVersion` set to something. For now, consider this version 0.1, so OpenBook requests should have the header set as following:

	"OpenBookVersion": "v0.1"

Note that version 0.1 is unstable, and might change. The next major version v0.2 will be stable for longer-term use.

### SSL Domain Identification

For most verbs and routes, hosts will demand encryption by redirecting to HTTPS. When a host connects to a peer, it will check its public key with its list of known hosts.

### Requests

Once you have a valid SSL certificate and can send HTTPS requests with the appropriate header, you can make OpenBook requests, of which there are two:

* [Getting Pages](Getting.md)

* [Posting to Pages](Posting.md)
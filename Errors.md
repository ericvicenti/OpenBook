# Errors in OpenBook

Clients detect errors primarly by response code. Errors are responses with codes 4XX or 5XX.

The response body should be an object if there was an error. The object will look like this:

```
  {
    message: 'Page not found',
    code: 404.00
    ... // machine-readable error attributes can go here
  }
```

A server does not need to send every error, but peers should properly interpret any of these official errors.

### Error Codes

Error codes are namespaced behind the http error code. IE. error 400.20 should be a 400 http response code, but also include the full error code in the response.

## Errors

### General Errors

Errors & codes for all types of [OpenBook requests](Requests.md).

#### 400.01 - Must use HTTPS

Sent to users trying to use HTTP or other protocols.

#### 400.02 - SSL Error

Error when unable to make a proper ssl connection. Usually this error will not be sent because the connection problem prevents any sending.

##### 400.03 - SSL Trust Error

Security chain is untrusted. Problem with key verification or the Certificate Authority.

#### 400.04 - Identity Error

The peer does not match the ssl identity, or the authenticated identity is not a super-peer of the specified peer.

This error is also used for posts with an invalid or unreadable peer specified.

#### 401.00 - Not Authorized

The requesting peer, whose identity is confirmed, is not authorized to perform this action. (GET or POST)

#### 404.00 - Page not found

No page can be found at this path.

### GET Errors

Learn more about [OpenBook GETs](Getting.md).

### POST Errors

Learn more about [OpenBook POSTs](Posting.md).

#### 400.20 - Cannot parse body

Sent when the POST body is unreadable as an array or an object.

#### 400.21 - Unacceptable Link

The link provided in the post object is unreadable, or links are not accepted.

This error should only ever occur when the link attribute is set in the post object.

#### 400.22 - Unacceptable opinion

Example:

```
{
  message: "Unacceptable opinion",
  code: 400.22,
  value: "like"
}
```

Unaccepted opinion. The officially supported opinions are 'like', 'dislike', and 'warn' (also null for no opinion).

The unaccepted opinion should be returned. This error should be used whenever the opinion field of a post object is deemed invalid.

Servers can use this message to say that a particular opinion is not accepted on its service.

This error should only ever occur when the opinion attribute is set in the post object.

#### 400.23 - Unacceptable subscription

The subscription value is unreadable or unacceptable. The server may not be accepting subscriptions.

This error should only ever occur when the subscription attribute is set in the post object.

#### 400.24 - Invalid target

The specified target of the post object is unreadable or not allowed.

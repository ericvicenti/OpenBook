### Getting Pages

A host provides an OpenBooks page a GET request. Hosts can serve traditional HTML sites alongside OpenBook pages, if it chooses.


A page is the name for a nugget of OpenBook content. They reside under any path under the host. For example, a blog page might be located at `https://first.last.name/blog/2012/hello_world`. A page can reside at any valid url under the host. 

A page contains the following in a JSON object:

* "title": String

  The title of the page, limited to 140 characters, which should not contain links or anything other than Unicode text


* "body": String

  The text body of the post, in [MarkShow](http://markshow.org/)


* "date": Integer

  A UNIX timestamp declaring when this page was last updated


* "context": String

  Optional link to context where this was posted


* "older": String

  Optional link to previous version of this page


* "newer": String

  Optional link to updated/ newer version of this page
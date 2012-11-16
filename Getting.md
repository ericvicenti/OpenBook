### Getting Pages

A host provides an OpenBooks page a GET request. Hosts can serve traditional HTML sites alongside OpenBook pages, if it chooses.


A page is the name for a nugget of OpenBook content. They reside under any path under the host. For example, a blog page might be located at `https://first.last.name/blog/2012/hello_world`. A page can reside at any valid url under the host. 

A page contains the following in a JSON object:

* "title": String

  The title of the page, limited to 140 characters, which should not contain links or anything other than Unicode text


* "body": String

  The URL where the content of the page can be found.


* "date": Integer

  A UNIX timestamp of the first pageing of this content

#webdev #REST #API 

# Everything is a Resource

Any interactions of a RESTful API is an interaction with a resource. In fact, the API can be considered simply as mapping an endpoint -- or, **resource identifier** (URL) to a resource. Resources are sources of information, typically documents or services. A user can be thought of as resource and this has an URL such as in the case of [GitHub](http://developer.GitHub.com/v3):

```
https://apt.github.com/users/lei
```

Resources can have different **representations**. 

The above mentioned user has the following JSON representation (partial document):

```JSON
{
	"login": "lrei",
	"created at": "2008-11-21T14:48:42Z",
	"name": "Luis Rei",
	"email": "me@luisrei.com",
	"id": 35857,
	"blog": "http://luisrei.com"
}
```
## Actions: HTTP Verbs and Response Codes

**Resources are nouns**. This fictional API URL:

```
http.api.example.com/posts/delete/233
```

Is wrong. It's obvious that *delete* is an action, not a resource. The way to do perform an action in a RESTful web service is to use HTTP **verbs** or **request methods**:

| HTTP Verb | Action (Typical Usage)                                                                                                             |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| GET       | Retrieves a representation of a resource without side effects (nothing changes on the server.)                                     |
| HEAD      | Retrieves just the resource meta-information (headers) i.e. same as GET but without the response body - also without side effects. |
| OPTIONS   | Returns the actions supported for specific resources - also without side effects                                                   |
| POST      | creates a resource.                                                                                                                |
| PUT       | (completely replaces an existing resource)                                                                                         |
| PATCH     | partial modification of a resource                                                                                                 |
| DELETE    | deletes a resource                                                                                                                 |
When using PUT, POST or PATCH, send the data as a document in the body of the request. Don't use query parameters to alter state. An example from the [GitHub API](http://developer.GitHub.com/v3):

```JSON
POST https://api.github.com/gists/gists
{
	"description": "the description for this gist"
	"public": true,
	"files": {
		"file1.txt": {
		"content": "String file contents"
		}
	}
	...
}
```

There's also a proper way to do **responses**: using the [HTTP Response Codes and Reason Phrase](http://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html#sec6.1.1). The reply to the previous request includes the following header:

```
201 Created
Location: https://api.github.com/gists/1
```

If one were to make the following request afterwards:

```
GET https://github.com/gists/1
```

The expected
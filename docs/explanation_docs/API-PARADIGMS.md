# API paradigms

Over the years, multiple API paradigms have emerged, being able able to
pick the right paradigm is important.
<br>In this article i explain the
paradigms you need to know about.

An API paradigm
defines the interface exposing backend data of a service to other
applications.

We can classify APIs into two categories:

- Request–Response APIs
- Event driven APIs

## Request–Response APIs

Request–response APIs typically expose an interface through an
HTTP-based web server.<br> APIs define a set of endpoints. Clients
make HTTP requests for data to those endpoints and the server
returns responses. <br>The response is typically sent back as JSON or
XML. There are three common paradigms used by services to
expose request–response APIs: REST, RPC, and GraphQL.

**1.Representational State Transfer**

Representational State Transfer (REST) is the most popular choice
for API development lately.<br> The REST paradigm is used by provid‐
ers like Google, Stripe, Twitter, and GitHub. REST is all about
resources.<br> A resource is an entity that can be identified, named,
addressed, or handled on the web.<br> REST APIs expose data as resour‐
ces and use standard HTTP methods to represent **Create,<br> Read,
Update, and Delete (CRUD)** transactions against these resources.<br>
For instance, Stripe’s API represents customers, charges, balance,
refunds, events, files, and payouts as resources.

Here are some general rules REST APIs follow:

- Resources are part of URLs, like /users.
  -For each resource, two URLs are generally implemented:<br> one
  for the collection, like /users, and one for a specific element,
  like /users/U123.
- Nouns are used instead of verbs for resources. <br>For example,
  instead of /getUserInfo/U123, use /users/U123.
- HTTP methods like **GET, POST, UPDATE**, and **DELETE** inform the
  server about the action to be performed.

Different HTTP meth‐
ods invoked on the same URL provide different functionality:
Create
Use POST for creating new resources.<br>
Read
Use GET for reading resources. GET requests never, ever
change the state of the resource. They have no side effects;
the GET method has a read-only semantic. GET is idempo‐
tent. <br>Consequently, you can cache the calls perfectly.
Update
Use PUT for replacing a resource and PATCH for partial
updates for existing resources.
Delete
Use DELETE for deleting existing resources.
• Standard HTTP response status codes are returned by the
server indicating success or failure. Generally, codes in the 2XX
range indicate success, 3XX codes indicate a resource has

**2.Remote Procedure Call**

Remote Procedure Call (RPC) is one of the simplest API paradigms,
in which a client executes a block of code on another server.
Whereas REST is about resources, RPC is about actions. Clients typ‐
ically pass a method name and arguments to a server and receive
back JSON or XML.
RPC APIs generally follow two simple rules:
• The endpoints contain the name of the operation to be exe‐
cuted.
• API calls are made with the HTTP verb that is most appropri‐
ate: GET for read-only requests and POST for others.
RPC style works great for APIs that expose a variety of actions that
might have more nuances and complications than can be encapsula‐
ted with CRUD or for which there are side effects unrelated to the
“resource” at hand. RPC-style APIs also accommodate complicated
resource models or actions upon multiple types of resources

**3. GraphQL**
GraphQL is a query language for APIs that has gained significant
traction recently. It was developed internally by Facebook in 2012
before being publicly released in 2015 and has been adopted by API
providers like GitHub, Yelp, and Pinterest. GraphQL allows clients
to define the structure of the data required, and the server returns exactly that structure.

```js{
 user(login: "saurabhsahni") {
 id
 name
 company
 createdAt
 }

Example  Response from GitHub GraphQL API
{
 "data": {
 "user": {
 "id": "MDQ6VXNlcjY1MDI5",
 "name": "Erick Njuki",
 "company": "Slack",
 "createdAt": "2009-03-19T21:00:06Z"
 }
 }
}
```

Unlike REST and RPC APIs, GraphQL APIs need only a single URL
endpoint. Similarly, you do not need different HTTP verbs to
describe the operation. Instead, you indicate in the JSON body
whether you’re performing a query or a mutation, as illustrated in
Example 2-7. GraphQL APIs support GET and POST verbs.
Example 2-7. GraphQL API call to GitHub

```js
POST /graphql
HOST api.github.com
Content-Type: application/json
Authorization: bearer 2332dg1acf9f502737d5e
 xoxp-16501860787-17163410960-113570727396-7051650
{
 "query": "query { viewer { login }}"
}
```

## Event-Driven APIs

With request–response APIs, for services with constantly changing
data, the response can quickly become stale. Developers who want
to stay up to date with the changes in data often end up polling the
API. With polling, developers constantly query API endpoints at a
predetermined frequency and look for new data,

To share data about events in real time, there are three common
mechanisms: WebHooks, WebSockets, and HTTP Streaming. We dive
deeper into each of them in the subsections that follow.
WebHooks
A WebHook is just a URL that accepts an HTTP POST (or GET, PUT,
or DELETE). An API provider implementing WebHooks will simply
POST a message to the configured URL when something happens.
Unlike with request–response APIs, with WebHooks, you can
receive updates in real time. Several API providers, like Slack, Stripe,
GitHub, and Zapier, support WebHooks. For instance, if you want to
keep track of “channels” in a Slack team with Slack’s Web API, you
might need to continuously poll the API for new channels.

**1. WebSockets**
WebSocket is a protocol used to establish a two-way streaming com‐
munication channel over a single Transport Control Protocol (TCP)
connection. Although the protocol is generally used between a web
client (e.g., a browser) and a server, it’s sometimes used for serverto-server communication, as well.
The WebSocket protocol is supported by major browsers and often
used by real-time applications. Slack uses WebSockets to send all
kinds of events happening in a workspace to Slack’s clients, includ‐
ing new messages, emoji reactions added to items, and channel crea‐
tions. Slack also provides a WebSocket-based Real Time Messaging
API to developers so that they can receive events from Slack in real
time and send messages as users. Similarly, Trello uses WebSockets
to push changes made by other people down from servers to brows‐
ers listening on the appropriate channels, and Blockchain uses its
WebSocket API to send real-time notifications about new transac‐
tions and blocks

utilizes the HTTP Streaming protocol to deliver data
through a single connection opened between an app and Twitter’s
streaming API. The big benefit for developers is that they don’t need
to poll the Twitter API continuously for new tweets. Twitter’s
Streaming API can push new tweets over a single HTTP connection
instead of a custom protocol. This saves resources for both Twitter
and the developer.
HTTP Streaming is easy to consume. However, one of the issues
with it is related to buffering. Clients and proxies often have buffer
limits. They might not start rendering data to the application until a
threshold is met. Also, if clients want to frequently change what kind
of events they listen to, HTTP Streaming might not be ideal because
it requires reconnections.

```

```

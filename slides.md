name: dblue

class: bg-dark-blue, center, middle
layout: true

---

name: green

class: green-template, center, middle
layout: true

---

name: lblue
layout: true

class: bg-light, center, middle

---

template: lblue
class: title

# Real-time Web Apps & Symfony.
# What are your options?

* <span class="speaker">Phil @leggetter</span>
* <span class="speaker-job-title">Head of Developer Relations</span>
* <span class="speaker-pusher-logo"></span>

???

---

template: lblue
class: bg-contain circles
background-image: url(./img/pusher-circles.png)

---

template: dblue
class: bg-dark-blue, h1-big

# Background

---

template: lblue

# Why Realtime?

???

* Here are some examples of apps...

---

template: dblue
class: em-text, bg-cover, trans-h, bottom
background-image: url(./img/itv-news-may-2014.png)

# Notifications & Signalling

???

* Something has happened
* Changed
* Alert - do something

---

class: bg-cover, em-text, trans-h, bottom
background-image: url(./img/delighted-app.gif)

# Activity Streams

???

* a stream of activity
* things have - and are - happening
* synonymous with social apps
  * Twitter
  * Facebook
  * Google+
  * News
  * Sports

---

template: dblue

class: bg-cover, em-text, trans-h, bg-white, bottom
background-image: url(./img/senate-election-results.png)

# Data Visualizations

---

template: lblue
class: bg-video, trans-h, em-text, bottom

# Chat

<video id="video" autoplay="true" loop="true">
  <source src="./img/pie.mp4" type="video/mp4">
</video>

???

* The 101 of realtime
* An interactive experience
* Real-time matters

---

class: bg-white
background-image: url(./img/messaging-apps.png)

---

template: dblue
class: trans-h, bg-cover, bottom
background-image: url(./img/uber.jpg)

# Real-Time Location Tracking

---

template: lblue
class: trans-h, bottom
background-image: url(./img/atom-pair.gif)

# Multi-User Collaboration

???

* Google Apps
* Cloud 9
* TODO: other

---

template: lblue
class: bg-cover, trans-h, bg-white, bottom
background-image: url(./img/quizup.png)

# Multiplayer Games

---

class: bg-pink, top

<img width="20%" src="./img/facebook.png" />
<img width="20%" src="./img/uservoice.png" />
<img width="25%" src="./img/google-docs.png" />
<img width="20%" src="./img/uber.png" />

--

# Users expect a real-time UX

--

# Without a real-time UX your app appears broken

---

class: bg-dark-blue, h1-big

# Real-time Web Apps & Symfony. What are your options?

---

template: lblue
class: h1-big, bg-cover, em-text
background-image: url(./img/falkirk-wheel.gif)

# 1. Use an existing solution

## Don't reinvent the wheel

<small>Unless you've a unique use case</small>

---

template: lblue

## Why use an existing solution?

* Fallback/upgrade hacks still required
* Support/Community
* Maintenance
* Future features
* Scaling

---

class: bg-white, bg-cover

background-image: url(./img/realtime-web-solutions-updated.png)

---

class: bg-cover, trans-h, top
background-image: url(./img/choose-a-lang.gif)

# 2. Use languages you're comfortable with

---

template: lblue
class: pinkie-bold

## Solutions by language

* **PHP**: ReactPHP, Ratchet
* **Java**: Netty, Jetty
* **JavaScript (Node.JS)**: Faye, Socket.IO (Engine.IO), Primus.io
* **.NET (C#)**: SignalR, XSockets
* **Python**: Lots of options built on Tornado
* **Ruby**: Faye
* *Language agnostic*: most hosted services

---

class: bg-pink

# [j.mp/realtime-tech-guide](j.mp/realtime-tech-guide)

---

template: dblue
class: h1-big, trans-h, bg-contain
background-image: url(./img/windows-apple-android.jpg)

# 3. Native Mobile Support?

---

template: lblue

## Native Mobile Support?

* Only some have mobile libraries
* How much data are you sending?
* SSL required on 3/4G networks
* HTTP fallback required?

---

template: lblue

## Solutions with Native Mobile Libraries

.left[* Faye
* Firebase
* Hydna
* PubNub]
.right[* Pusher
* Realtime
* SignalR
* Socket.IO]

---

template: dblue
class: h1-big

# 4. Application/Solution Functionality 

---

template: lblue

## 4. Application/Solution Functionality

* Information Architecture a.k.a Data
* Interaction/Communication Complexity:
  * How users interact with your app
  * Client <-> Server interactions
* Understand the framework functionality you need...

???

* Going back to the 4 data paradigms:
* Do you want a few simple streams of data - onMessage
* Are there multiple streams where the app chops and changes the information it wants - PubSub
* Do you need bi-directional communication?
* Are you effectively manipulating a share data structure - sync
* Or are you trying to provide access to server functionality in a more elegant way - RMI

---

class: bg-pink

# Functionality, huh?!

--

# Communication Patterns

---

template: lblue
class: left-content, code-reveal, top

## onMessage

```js
// client

var sock = new SockJS( 'http://localhost:9999/sockjs' );
```
--

```
sock.onmessage = function( e ) {
  console.log( 'message', e.data );
};
```
--
<hr />
```js
// server

sock.write( 'hello SockJS' );
```

---

template: lblue
class: code-reveal, top

## PubSub

```js
// client

var client = new FayeClient();
```
--

```
client.subscribe( 'messages', function( message ) {
  // Handle Update
} );
```
--
<hr />

```js
// server

var message = {
  text: 'Hello, world!',
  user_name: '@leggetter'
}
Faye.publish( 'messages', message );
```

---

template: lblue
class: code-reveal, top

## Evented PubSub

```js
// client

var pusher = new Pusher( APP_KEY );
```
--

```js
var channel = pusher.subscribe( 'chat' );
```
--
```js
channel.bind( 'message', function( data ) {
  // Handle Update
} );
```
--

```
channel.bind( 'message-updated', function( data ) {} );

channel.bind( 'room-name-changed', function( data ) {} );
```
--
<hr />

```js
// server

var data = [
  'text' => 'Hello, world!',
  'user_name' => '@leggetter'
}
pusher->trigger( 'chat', 'message', data );
```

---

template: lblue
class: code-reveal, top

## Data Sync

```js
var myDataRef = new Firebase('https://yo.firebaseio.com/');
```
--

```
myDataRef.push( {name: '@leggetter', text: 'Yo!'} );
```
--

```
myDataRef.on( 'child_added', function(snapshot) {
  // Data added
});

myDataRef.on( 'child_changed', function(snapshot) {
  // Data has changed
});

myDataRef.on( 'child_removed', function(snapshot) {
  // Data removed
});
```

???

* Manipulating collection of data
* Not dealing with Messages

---

template: lblue
class: top, code-reveal, long, wide

## RMI

```js
// client

$.connection.hub.start(); // async
```
--

```js
var chat = $.connection.chatHub;
```
--

```js
chat.client.broadcastMessage = function (name, message) {
  // handle message
};
```
--

```js
chat.server.send( 'me', 'hello world' );
```
--
<hr />

```csharp
// server

public class ChatHub : Hub
{
```
--

```csharp
  public void Send(string name, string message)
  {
```
--

```csharp
    // Call the broadcastMessage method to update clients.
    Clients.All.broadcastMessage(name, message);
  }
}
```

---

template: lblue
class: bg-white
background-image: url(./img/rtw-tech-decision-matrix-black.png)

---

class: bg-white
background-image: url(./img/rtw-tech-decision-matrix-apps-black.png)

???

  
---

class: bg-white
background-image: url(./img/rtw-tech-decision-matrix-solutions-white.png)

???
  
* SockJS - focus on simple connections
* Some solutions offer PubSub and data sync
* Dropbox - offer simple DataStore API
* Only know a few RMI options
* New solutions: Meteor, DerbyJS, SailsJS - maybe a new category for these?

---

template: dblue
class: h1-big

# 5. Where are you in Development?

---

template: lblue

# You are just starting out
    
* Architecture considerations
* Go all-in with a "new breed of framework"

---

template: lblue
class: fixed-width-list

### Realtime Framework
    
* Meteor & hosted offering
* SailsJS
* SocketStream

### BaaS (Back-end as a Service)

* Firebase
* Syncano
* ...

See: [nobackend.org](http://nobackend.org/) & [j.mp/realtime-tech-guide](http://j.mp/realtime-tech-guide)
    
???

* A Framework where you can self-host
* Or hosted service: a BaaS where your can focus mainly on front-end functionality
* In both cases: Realtime is baked in
* In some cases even HTML templating will be baked in
* and those templates will auto-updated when you update data structures
* Will "Realtime" simply become an expected piece of functionality in the same way we expect to be able to persist data?

---

template: lblue

# You already have an app
    
* How to integrate:
  * Self-hosted
  * Hosted

---

template: lblue
class: bottom
background-image: url(./img/realtime-web-stack-tight-integration-self-hosted.png)

### Self Hosted <small>(Tightly Coupled)</small>


???

* Less initial overhead - quick Integration
* As project grows complexity increases
* Updating request/response cycle may impact realtime functionality and vise-versa
* Likely that the web server is handling load of both standard HTTP and realtime i.e. WebSocket, Server-Sent Events, HTTP fallbacks

---

## PHP Self-Hosted Tightly Coupled options

* [React (PHP)](http://reactphp.org/)
  * Event-driven, non-blocking I/O with PHP.
* [Ratchet](http://socketo.me/) (Built on React PHP)
  * WebSockets, WAMP, PubSub samples. No HTTP Fallback
* [phpDaemon](http://daemon.io/)
  * Lots of examples. Most docs in Russian.

???

* React: Event-driven, non-blocking I/O with PHP.
* Ratchet: WebSockets, WebSocket Application Messaging Protocol, PubSub examples and more. Not HTTP fallback

---

> Yes it’s possible but not common or probably recommended yet. There are some projects that are starting to do this by running the HTTP stack on React [...] but it’s very uncommon at this point in time

[Chris Boden](https://twitter.com/boden_c), Creator/Maintainer of React (PHP) & Ratchet

---

template: lblue
class: bottom
background-image: url(./img/realtime-web-stack-integration-self-hosted.png)

### Self Hosted <small>(Loosely Coupled)</small>

???
  
* Generally agreed that a loosely coupled architecture is going to be easier to change and maintain
* Your DB may even be message-queue-capable e.g. Redis.
* So you simply need to hook your realtime server into that
* Web App for HTTP
* Realtime for realtime functionality
* Scale-out realtime server in the same way as web server

---

## PHP Self-Hosted Loosely Coupled options

* Anything!

---

template: lblue
class: bottom
background-image: url(./img/realtime-web-stack-integration-hosted.png)

### Hosted

???

---

template: dblue

# 6. Self-Hosted v Hosted

## "Build vs. Buy"

---

template: green
class: trans-h bottom
background-image: url(./img/realtime-web-stack-integration-self-hosted-symfony-ratchet.png)

## Self-Hosted Demo 1: Symfony + Ratchet

---

## Self-Hosted Demo 1 - Pro & Cons

.left[
**Pros**

* PHP
* Simple integration
* Standards-based
  * WAMP/Autobahn
  * JS, Android, iOS & more
]

.right[
**Cons**

* No HTTP fallback
* Low-level abstractions
* Different programming style
* You need to scale
]

---

template: green
class: trans-h bottom
background-image: url(./img/realtime-web-stack-integration-self-hosted-symfony-faye.png)

## Self-Hosted Demo 2: Symfony + Faye

---

## Self-Hosted Demo 2 - Pro & Cons

.left[
**Pros**

* In-build Redis/Queue support
* PubSub
* Simple integration
]

.right[
**Cons**

* Not PHP(?)
* You need to scale
]

---

template: green
class: bottom trans-h
background-image: url(./img/realtime-web-stack-integration-hosted-symfony-pusher.png)

# Hosted Demo: Pusher

---

## Hosted - Pros & Cons


.left[
**Pros**

* Instantly scalable
* Managed & dedicated
* Direct integration into Symfony
]

.right[
**Cons**

* 3rd party reliance
]

???

* Load-balancing connections
* Maintaining state of connections
* Synchronising data between nodes
* Mapping connections to users?
* Dedicated hosted service will offer :
  * Make things easier and faster  
  * Reduce scaling complexities
  * Natural loose coupling via an API
* Where is your value?
  * Features v Infrastructure

---

class: bg-cover top trans-h
background-image: url(img/build-vs-buy.png)

## Build vs. Buy - Costs

<a class="bg-pink" style="position: absolute; top: 2%;" href="https://baremetrics.com/calculator">baremetrics.com/calculator</a>

---

template: dblue

## How do you choose?
### 6 Realtime Framework Considerations

1. Use an Existing Solution
2. Use a language you're comfortable with
3. Do you need native mobile support?
4. onMessage, PubSub (Evented), RMI or DataSync
5. Where in development?
6. Hosted v Self-Hosted (Build vs. Buy)

---

class: bg-pink

# You need Real-Time!

## Make the choice that's right for you!

---

# Resources

* [Real-time Tech Guide](http://j.mp/realtime-tech-guide)
* [React (PHP)](http://reactphp.org/)
* [Ratchet (PHP)](http://socketo.me/)
* [Faye (Node/Ruby)](http://faye.jcoglan.com/)
* [Pusher](https://pusher.com)

---

class: title

# Real-time Web Apps & Symfony.
# What are your options?

## Questions?

[leggetter.github.io/realtime-symfony](leggetter.github.io/realtime-symfony)

* <span class="speaker">Phil @leggetter</span>
* <span class="speaker-job-title">Head of Developer Relations</span>
* <span class="speaker-pusher-logo"></span>

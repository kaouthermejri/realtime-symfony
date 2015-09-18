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

class: fixed-width-list

## What we'll cover

1. Why Real-Time?
2. What are your options
  * How do you choose?
  * Pros & Cons
3. 3 Example Solutions for Symfony

---

template: dblue
class: bg-dark-blue, h1-big

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
class: bg-cover, trans-h, bg-white
background-image: url(./img/lunar-landing.png)

<h3 style="position: absolute; top: 2%; right: 2%; display: inline-block";>
  Multiplayer Games /<br />
  "Do some real-time art!"
</h3>

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

template: dblue
class: h1-big

# Real-time Web Apps & Symfony. What are your options?

---

class: bg-pink, h1-big

# 6 Factors to Consider

---

template: dblue
class: h1-big, bg-cover, em-text
background-image: url(./img/falkirk-wheel.gif)

# 1. Use an existing solution

## Don't reinvent the wheel

<small>Unless you've a unique use case</small>

---

template: lblue
class: fixed-width-list

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

template: dblue
class: bg-cover, trans-h, top
background-image: url(./img/choose-a-lang.gif)

# 2. Use languages you're comfortable with

---

template: lblue
class: pinkie-bold

## Solutions by language

* **PHP**: ReactPHP, Ratchet, dNode-php, phpDaemon
* **Java**: Netty, Jetty
* **JavaScript (Node.JS)**: Faye, Socket.IO (Engine.IO), Primus.io
* **.NET (C#)**: SignalR, XSockets
* **Python**: Lots of options built on Tornado
* **Ruby**: em-websocket, Faye
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

---

template: lblue

## Solutions with Native Mobile Libraries

.left[* Faye
* Firebase
* Hydna
* PubNub]
.right[* Pusher
* Ratchet (via Autobahn)
* SignalR
* Socket.IO]

---

template: dblue
class: h1-big

# 4. Application/Solution Functionality 

---

class: bg-pink

# Functionality, huh?!

--

# Communication Patterns

???

Let me clarify this with code.

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
client.subscribe( 'chat', function( message ) {
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
Faye.publish( 'chat', message );
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
class: top, code-reveal, long

## RMI

```js
// client

$.connection.hub.start(); // async

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

# 5. Architecture Considerations

---

template: lblue
class: bg-pink fixed-width-list

## I wanna build a real-time Symfony app
or
## I wanna add real-time to an existing Symfony app

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

## PHP Self-Hosted options

* [React (PHP)](http://reactphp.org/)
  * Event-driven, non-blocking I/O with PHP.
* [Ratchet](http://socketo.me/) (Built on React PHP)
  * WebSockets, WAMP, PubSub samples. No HTTP Fallback
* [dnode-php (RPC/RMI)](https://github.com/bergie/dnode-php)
* [phpDaemon](http://daemon.io/)
  * Lots of examples. Most docs in Russian.

???

* Ratchet: WebSockets, WebSocket Application Messaging Protocol, PubSub examples and more. Not HTTP fallback

---

> Yes it’s possible but not common or probably recommended yet. There are some projects that are starting to do this by running the HTTP stack on React [...] but it’s very uncommon at this point in time

[Chris Boden](https://twitter.com/boden_c), Creator/Maintainer of React (PHP) & Ratchet

---

template: green
class: bottom, trans-h
background-image: url(./img/realtime-web-stack-integration-self-hosted-symfony-ratchet.png)

???
  
* Generally agreed that a loosely coupled architecture is going to be easier to change and maintain
* Your DB may even be message-queue-capable e.g. Redis.
* So you simply need to hook your realtime server into that
* Web App for HTTP
* Realtime for realtime functionality
* Scale-out realtime server in the same way as web server

--

### Self-Hosted Demo 1: Symfony + Ratchet <small>(Loosely Coupled)

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
class: bottom, trans-h
background-image: url(./img/realtime-web-stack-integration-self-hosted-symfony-faye.png)

--

### Self-Hosted Demo 2: Symfony + Faye <small>(Loosely Coupled)

---

## Self-Hosted Demo 2 - Pro & Cons

.left[
**Pros**

* PubSub
* Connection fallback
* In-build Redis/Queue support
* Simple integration
]

.right[
**Cons**

* Not PHP(?)
* You need to scale
]

---

template: green
class: bottom, trans-h
background-image: url(./img/realtime-web-stack-integration-hosted-symfony-pusher.png)

--

### Hosted Demo: Pusher

---

## Hosted - Pros & Cons


.left[
**Pros**

* Simple & powerful
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

template: dblue

# 6. Self-Hosted v Hosted

## "Build vs. Buy"

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
5. Architectural considerations
6. Hosted v Self-Hosted (Build vs. Buy)

---

class: bg-pink

# You need Real-Time!

## There are lots of options.

## Make the choice that's right for you.

## I hope this helps!

---

class: fixed-width-list

# Resources

* [Real-time Tech Guide](http://j.mp/realtime-tech-guide)
* [React (PHP)](http://reactphp.org/)
* [Ratchet (PHP)](http://socketo.me/)
* [Faye (Node/Ruby)](http://faye.jcoglan.com/)
* [Pusher](https://pusher.com)
* [LopiPusherBundle](https://github.com/laupiFrpar/LopiPusherBundle)
* [github.com/leggetter/realtime-symfony-examples](https://github.com/leggetter/realtime-symfony-examples)

---

class: title

## Real-time Web Apps & Symfony.</br>What are your options?

### Questions?

[joind.in/14980](https://joind.in/14980) | [leggetter.github.io/realtime-symfony](leggetter.github.io/realtime-symfony)

* <span class="speaker">Phil @leggetter</span>
* <span class="speaker-job-title">Head of Developer Relations</span>
* <span class="speaker-pusher-logo"></span>

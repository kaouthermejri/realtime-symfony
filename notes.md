* http://knpbundles.com/search?q=real-time
* http://www.slideshare.net/Xosofox/real-time-event-dispatcher
* http://arbrand.es/2013/04/16/optimizing-a-real-time-symfony-app-with-memcached-socket-io-node-js-redis-and-nginx/
* http://jwage.com/post/30490209661/asynchronous-events-with-php-and-symfony2
* https://philsturgeon.uk/php/2013/11/12/benchmarking-codswallop-nodejs-v-php/

## Symfony + Faye

* Faye Symfony Bundle: https://github.com/cravler/CravlerFayeAppBundle
* Faye Node app: https://github.com/cravler/faye-app
* Blog: http://devblog.lexik.fr/symfony2/notifications-via-websocket-avec-symfony2-et-node-js-2679

---

Demos:

## Ratchet

1. Show sample app working in two windows. Post message. Doesn't appear in other window - need to refresh or poll.

2. Let's use Ratchet. To do this we're doing to need Redis running. It is.

3. Let's publish the message we recieve to Redis.

```
sym-redis
```

4. Show Ratchet code:

* bin/chat-server.php
* Creating a new chat instance
* Passing in to Ratchet WsServer so it can get WS events
* Creating a redis client to receive events from our symfony app
* Initing the Chat app with the Redis instance
* Some crazy stuff going on around `$server->loop` - we can let Ratchet handle that.
* In `Chat.php`:
  * Collect incoming WebSocket connections
  * Subscribe to `chat` channel
  * When we receive messages from Redis we send to each client
  
5. Show the demo by going to http://localhost:8000/chat/ratchet/ and show demo in two windows
  
## Faye

1. Since we've got a nice loosely coupled system we can actually swap out Ratchet for another solution and continue to use the Redis message queue. This time let's go with Faye by James Coglan. Faye is available for Node and Ruby. In this sample I'll use Node.

2. Talk through `faye/index.js`

3. Stop the Ratchet example and run `faye/index.js`

4. Navigate to http://localhost:8000/chat/faye/ and show demo in two windows

## Pusher

1. Finally, here's how to integrate a hosted service such as Pusher. In this case we don't need a message queue so we can kill that. And we don't need a second service. Pusher replaces both of these components.

2. Open up `ChatController.php` and replace the Redis queuing code with the Pusher code.

3. Navigate to http://localhost:8000/chat/pusher/ in both windows

4. Run ngrok -subdomain=pusher 8000 and ask people to go to pusher.ngrok.com/chat/pusher

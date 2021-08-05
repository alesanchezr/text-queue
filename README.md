# Text-Based-Queue

Extremelly simple text-based polling queue engine. Similar to a socket but simpler, text-based and unidirectional (polling protocol).

## What is this for?

Is a simpler alternative to Socket.io with less restrictions.
- Some times using sockets is impossible because of security or network limitations.
- Faster than sockets
- Persistent (if option.create = false the queue history will never be deleted)

## How to use

1. Initializing a new queue and dispatiching your first event:

```js
// initialize your dispatcher
const dispatcher = queue.dispatcher({ create: true, path: `./path/to/file.json` })

//you can send any data as event payload
let data = { foo: "bar" }
// start enqueing/dispatching any events
dispatcher.enqueue("initilialized", data)


// dispatch any other custom event you want
dispatcher.enqueue("send_email")
```


2. Listening to incoming events from the queue:

```js
  //initialize your queue listener
  const listener = queue.listener({ path: `./path/to/file.json` })
  
  // when a new event is added to the queue, the onPull method will be triggered 
  // and you receive the incoming event name and the payload/data
  listener.onPull((e) => console.log(`Incoming event with name ${e.name}`, e.data))
  
  // if the queue file gets deleted or reseted we can also listen and receive any queued events
  listener.onReset((e) => console.log(`Incoming event with name ${e.name}`, e.data))
```

## Options and Settings

### For the queue dispatcher

```js
queue.dispatcher({ 
  create: true, // Will create a new queue every time its initialized, defaults to false
  path: `./path/to/file.json` // path to the file that will store the queue
})
```


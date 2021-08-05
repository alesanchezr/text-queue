# Text Queue

Text-based queue management simplified

## How to use

1. Initializing a new queue and dispatiching your first event:

```js
// initialize your dispatcher
const dispatcher = queue.dispatcher({ create: true, path: `./path/to/file/vscode_queue.json` })

// start enqueing/dispatching any events
dispatcher.enqueue("initilialized", req.params.slug)


// dispatch any other custom event you want
dispatcher.enqueue("send_email", req.params.slug)
```


2. Listening to incoming events from the queue:

```js
  //initialize your listener
  let listener = queue.listener({ path: `./path/to/file/vscode_queue.json` })
  
  // when a new event is added to the queue, the onPull method will be triggered
  listener.onPull((e) => console.log(`Incoming event with name ${e.name}`, e.data))
  
  // if the queue file gets deleted or reseted we can also listen and receive any queued events
  listener.onReset((e) => console.log(`Incoming event with name ${e.name}`, e.data))
```

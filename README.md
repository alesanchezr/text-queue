# Text Queue

Text-based queue management simplified

## How to use

1. Initializing a new queue and dispatiching your first event:

```js
// initialize your dispatcher
const dispatcher = queue.dispatcher({ create: true, path: `${config.dirPath}/vscode_queue.json` })

// start enqueing/dispatching any events
dispatcher.enqueue(dispatcher.events.START_EXERCISE, req.params.slug)
```


2. Listening to incoming events from the queue:

```js
  //initialize your listener
  let listener = queue.listener({ path: `${extension.workspaceRoot}/${configFile.config.dirPath || ".learn"}/vscode_queue.json` })
  
  // when a new event is added to the queue, the onPull method will be triggered
  listener.onPull((e) => console.log(`Incoming event with name ${e.name}`, e.data))
  
  // if the queue file gets deleted or reseted we can also listen and receive any queued events
  listener.onReset((e) => console.log(`Incoming event with name ${e.name}`, e.data))
```


### process-message

process-message is a magical module. The magic is that you don't need to know it exists.

```js
// index.js
const cp = require('child_process');
const Msg = require('process-message');

const worker = co.fork('./worker.js');
const msg = new Msg(worker);

msg.emit('hello', { name: 'xiaoming' });        // main -> child
msg.on('world', data => {                       // child -> main
    console.log(data.name);     // xiaoming
});
```

```js
// worker.js
const Msg = require('process-message');
const msg = new Msg(process);

msg.on('hello', data => {                       // main -> child
    console.log(data.name);     // xiaoming
    msg.emit('world', data);                    // child -> main
});
```

**Node Getting Started!**
===================



----------


First things first! Choose an editor.
-------------

I'll make it easy VS Code[A great lightweight editor with a ton of plugins.](https://code.visualstudio.com/)

**Standardize Layout**
In VS config add the editorconfig plugin [learn more](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)

[NSP Check node packages for security issues.](https://nodesecurity.io/)
npm install -g nsp
nsp check 


**Share your application with others using** 
now, surge, localtunnel, surge
Using local tunnel
npm install localtunnel -g
$lt -p 3000
>your url is: https://jrhibrpclw.localtunnel.me -- these will be created dynamically

**NPM Scripts**
 "scripts": {
    "start": "npm-run-all --parallel security-check start-up",
    "prestart": "babel-node build-scripts/startMsg.js", //babel-node
    "start-up": "babel-node build-scripts/srcServer.js",
    "security-check": "nsp check",
    "localtunnel": "lt -p 3000",
    "share": "npm-run-all --parallel security-check start-up localtunnel"
    "clean-dist": "rimraf ./dist && mkdir dist",
     "lint": "esw webpack.config.* src buildScripts --color",
    "lint:watch": "npm run lint -- --watch",
  },
  Note that babel is a transpiler to shim in new feature for ES support

**RIMRAF.js**
rm -rf -- recursively remove files

**ESLINT**

**Testing**
Mocha
Chai
JSDOM
Travis CI
Ad .travis.yml to the root of your pj
.travis.yml
language: node_js
node_js:
  - "7"

StackEdit
StackEdit stores your documents in your browser, which means all your documents are automatically saved locally and are accessible **Child_process!**

Is used to start new threads
exec
spawn
fork

Download this package create a threads folder
bootstrapzero.com to get themes

node --version

**Node REPL**

**NODE EVENT LOOP**

Node's "event loop" is central to being able to handle high throughput scenarios. It is a magical place filled with unicorns and rainbows, and is the reason Node can essentially be "single threaded" while still allowing an arbitrary number of operations to be handled in the background. This post will shed light on how the event loop operates so you too can enjoy the magic.



The 'fs' module mostly uses the error back callback style. It would technically be possible to emit additional events for some calls, such as fs.readFile(), but the API was made to only alert the user if the desired operation succeeded or if something failed. This API selection was an architecture decision and not due to technical limitations.

A common misconception is that event emitters are somehow asynchronous in nature on their own, but this is incorrect. The following is a trivial code snippet to demonstrate this.

~~~
`function MyEmitter() {

  EventEmitter.call(this);
  
}

util.inherits(MyEmitter, EventEmitter);

MyEmitter.prototype.doStuff = function doStuff() {

  console.log('before')

  emitter.emit('fire')

  console.log('after')}

};

var me = new MyEmitter();

me.on('fire', function() {

  console.log('emit fired');

});


me.doStuff();

// Output:

// before

// emit fired

// after
~~~


EventEmitter often appears asynchronous because it is regularly used to signal the completion of asynchronous operations, but the EventEmitter API is entirely synchronous. The emit function may be called asynchronously, but note that all the listener functions will be executed synchronously, in the order they were added, before any execution can continue in statements following the call to emit.

Node itself depends on multiple libraries. One of those is libuv, the magical library that handles the queueing and processing of asynchronous events. For the remainder of this post please keep in mind that I won't distinguish if a point made relates directly to Node or libuv.
Node utilizes as much of what's already available from the operating system's kernel as possible. Responsibilities like making write requests, holding connections and more are therefore delegated to and handled by the system. For example, incoming connections are queued by the system until they can be handled by Node.
You may have heard that Node has a thread pool, and might be wondering "if Node pushes all those responsibilities down why would a thread pool be needed?" It's because the kernel doesn't support doing everything asynchronously. In those cases Node has to lock a thread for the duration of the operation so it can continue executing the event loop without blocking.



**REQUIRE**

used to access modules

var os = require('OS'); // this module can give you info about your underlying OS

module.exports is a property used to export elemements of a module


**Callbacks vs Events**

~~~
var events = require('events');

var eventCenter = new events.EventEmitter();

eventCenter.on('init', function() {
    var greeting = 'Hello World!';
    console.log('We're in the init function!);
    eventCenter.emit('secondFunction', greeting);
});

eventCenter.on('secondFunction', function(greeting) {
        console.log('We're in the second function!);
        console.log(greeting);
    eventCenter.emit('nextFunction');
});

eventCenter.on('nextFunction', function {
    /* do stuff */
});

eventCenter.emit('init');

~~~

The nice thing about callbacks is there's no global state there, and passing parameters to them is trivial. If you have a function download(URL, callback: (FileData)->void) then you can know that's a self-contained higher-order function which essentially lets you construct a "grab this and do that" function. 

~~~
var myCallback = function(err, data) {
  if (err) throw err; // Check for the error and throw if it exists.
  console.log('got data: '+data); // Otherwise proceed as usual.
};

var usingItNow = function(callback) {
  callback(null, 'get it?'); // I dont want to throw an error, so I pass null for the error argument
};
If we want to simulate an error case, we can define usingItNow like this

var usingItNow = function(callback) {
  var myError = new Error('My custom error!');
  callback(myError, 'get it?'); // I send my error as the first argument.
};
The final usage is exactly the same as in above:

usingItNow(myCallback);
~~~

The only difference in behavior would be contingent on which version of usingItNow you've defined: the one that feeds a "truthy value" (an Error object) to the callback for the first argument, or the one that feeds it null for the error argument.

Node blocking code
~~~
var fs = require("fs");

var data = fs.readFileSync('input.txt');

console.log(data.toString());
console.log("Program Ended");
~~~


Non blocking

~~~
var fs = require("fs");

fs.readFile('input.txt', function (err, data) {
   if (err) return console.error(err);
   console.log(data.toString());
});

console.log("Program Ended");
~~~

The child process module

1. execFile
What?

Executes an external application, given optional arguments and callback with the buffered output after the application exits.

~~~
Running the below code will print out the current node version.

const execFile = require('child_process').execFile;
const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
        console.error('stderr', stderr);
        throw error;
    }
    console.log('stdout', stdout);
});
~~~

When?

execFile is used when we just need to execute an application and get the output. For example, we can use execFile to run an image-processing application like ImageMagick to convert an image from PNG to JPG format and we only care if it succeeds or not. execFile should not be used when the external application produces a large amount of data and we need to consume that data in real time manner.

**2. spawn**

What?

The spawn method spawns an external application in a new process and returns a streaming interface for I/O.

How?

**3 exec**



~~~
const spawn = require('child_process').spawn;
const fs = require('fs');
function resize(req, resp) {
    const args = [
        "-", // use stdin
        "-resize", "640x", // resize width to 640
        "-resize", "x360<", // resize height if it's smaller than 360
        "-gravity", "center", // sets the offset to the center
        "-crop", "640x360+0+0", // crop
        "-" // output to stdout
    ];
    const streamIn = fs.createReadStream('./path/to/an/image');
    const proc = spawn('convert', args);
    streamIn.pipe(proc.stdin);
    proc.stdout.pipe(resp);
}
~~~

In the Node.js function above (an express.js controller function), we read an image file using a stream. Then, we use spawn method to spawn convert program (see imagemagick.org). Then, we feed ChildProcess proc with the image stream. As long as the proc object produces data, we write that data to the resp (which is a Writable stream) and users can see the image immediately without having to wait for the whole image to convert (resized).


**When?**

As spawn returns a stream based object, it’s great for handling applications that produce large amounts of data or for working with data as it reads in. As it’s stream based, all stream benefits apply as well:

Low memory footprint

Automatically handle back-pressure

Lazily produce or consume data in buffered chunks.

Evented and non-blocking

Buffers allow you to work around the V8 heap memory limit


***3 exec***
~~~

var child = require('child_process');
child.exec('uptime', function (error, stdout, stderr) {
    console.log(stdout);
});

~~~

spawn(command, [args], [options] )
~~~
const exec = require('child_process').exec;
exec('cat *.js bad_file | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`exec error: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.log(`stderr: ${stderr}`);
});

const execFile = require('child_process').execFile;
const child = execFile('node', ['--version'], (error, stdout, stderr) => {
  if (error) {
    throw error;
  }
  console.log(stdout);
});
~~~

Fork

fork is built on spawn but designed to run node applications
For example, if you have the following two files:


In main.js:
~~~
var cp = require('child_process');
var child = cp.fork('./worker');

child.on('message', function(m) {
  // Receive results from child process
  console.log('received: ' + m);
});

// Send child process some work
child.send('Please up-case this string');
In worker.js:

process.on('message', function(m) {
  // Do work  (in this case just up-case the string
  m = m.toUpperCase();

  // Pass results back to parent process
  process.send(m.toUpperCase(m));
});
~~~

Cluster

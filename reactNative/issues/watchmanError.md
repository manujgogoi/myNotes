# Watchman Error on Macbook:

Error Output:

```sh
metro-file-map: Watchman crawl failed. Retrying once with node crawler.
  Usually this happens when watchman isn't running. Create an empty `.watchmanconfig` file in your project's root folder or initialize a git or hg repository in your project.
  Error: Watchman error: std::__1::system_error: open: /Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject: Operation not permitted. Make sure watchman is running for this project. See https://facebook.github.io/watchman/docs/troubleshooting.
node:events:492
      throw er; // Unhandled 'error' event
      ^

Error: std::__1::system_error: open: /Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject: Operation not permitted
    at BunserBuf.<anonymous> (/Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject/node_modules/fb-watchman/index.js:99:23)
    at BunserBuf.emit (node:events:514:28)
    at BunserBuf.process (/Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject/node_modules/bser/index.js:292:10)
    at /Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject/node_modules/bser/index.js:247:12
    at process.processTicksAndRejections (node:internal/process/task_queues:77:11)
Emitted 'error' event on WatchmanWatcher instance at:
    at Client.<anonymous> (/Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject/node_modules/metro-file-map/src/watchers/WatchmanWatcher.js:86:12)
    at Client.emit (node:events:514:28)
    at BunserBuf.<anonymous> (/Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject/node_modules/fb-watchman/index.js:111:12)
    at BunserBuf.emit (node:events:514:28)
    at /Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject/node_modules/bser/index.js:249:12
    at process.processTicksAndRejections (node:internal/process/task_queues:77:11) {
  watchmanResponse: {
    error: 'std::__1::system_error: open: /Users/manuj/Documents/official/webxplanet/practice/RN/AwesomeProject: Operation not permitted',
    version: '2023.12.04.00'
  }
}

Node.js v20.10.0
Process terminated. Press <enter> to close the window
```

## Solution

Move the project from `Documents` directory to users directory.
In my case I moved the project dir to `/Users/manuj/RNProjects/Test/AwesomeProject`

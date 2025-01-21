# Intermittent Node.js Server Crash

This repository demonstrates a common yet tricky bug in Node.js: an intermittent server crash without informative error messages.  The server, implemented using the built-in 'http' module, randomly stops responding. This bug is difficult to debug because it doesn't produce traditional error logs.

## Bug Description
A simple HTTP server is created. Under load, or sometimes randomly, the server ceases to respond to new requests.  No exceptions are thrown or logged to the console, making the root cause elusive. The provided `server.js` file contains the problematic code. `serverSolution.js` demonstrates a solution to handle uncaught exceptions more gracefully.

## How to Reproduce
1. Clone the repository.
2. Run `node server.js`.
3. Send numerous requests to the server using tools like `curl` or a load testing tool.
4. Observe the server's behavior over time; it may stop responding at an unpredictable point without an error message.

## Solution
The solution, detailed in `serverSolution.js`, involves using process.on('uncaughtException') to handle unhandled exceptions and prevent the server from silently crashing. This allows the server to gracefully handle unexpected errors and keep running despite encountering them, logging them so the issue can be diagnosed.
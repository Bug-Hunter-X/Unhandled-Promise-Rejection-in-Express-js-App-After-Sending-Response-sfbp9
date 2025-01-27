# Unhandled Promise Rejection in Express.js After Sending Response

This repository demonstrates a subtle but important error handling issue in Node.js Express.js applications.  The problem arises when an asynchronous operation within a route handler throws an error *after* the response has already been sent to the client.  In such cases, the error might not be caught by standard `try...catch` blocks, leading to an unhandled promise rejection and potential instability.

## Reproducing the Bug

1. Clone the repository.
2. Run `npm install` to install the Express.js dependency.
3. Run `node bug.js`. 
4. Refresh the page several times. You will occasionally see an error in the console that doesn't interrupt the server process, but indicates a potential issue.

## Solution

The solution is to ensure proper error handling even after sending the response. In the solution file, we use a `process.on('unhandledRejection', ...)` listener to gracefully handle such cases.  This is a good practice for production applications.

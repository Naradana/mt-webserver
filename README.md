# mt-webserver
Multi-threading Web Server for node.js

While node.js is very successful to implement webserves to handle quite simple calls efficiently, but programming database applications with complex transactions spanning multiple tables becomes quite difficult to write. The multi-threading web server allows to program applications in the classical object-oriented/procedural style.

Problems with node:

-   complex sequential procedurs require extensive additional programming effort to not block the main thread
-   intuitive procedural OO programming is not possible - the beauty of the easy to learn and to use JavaScript programming language is lost
-   a single error in the main thread can halt or impair the whole application
-   the main thread becomes easily a bootleneck for the whole system
-   the programmer must make sure that the garbage collection really can clean up or the node process RAM usage increases over time

Solution:

+   starting a new thread for reasonable complex request handlers
+   other requests are handled asap with standard node techniques
+   the main thread works as HTTP router distributing requests to HTTP handler threads
+   a thread pool helps to minimize start-up time
+   optional caching the HTTP response into RAM or to file system fastens subsequent calls
+   a shared ACID key/value store makeing data exchange between threads easy

Drawbacks:

*   Starting a new thread is expensive, so it should not be used for every minor HTTP request
*   Most existing libraries are designed with callbacks and heavily used libs should have some simple wrapper to hide their asynchronous behavior for devlopers
    not comfortable with async and promises, so they can stick to strict procedural programming

## Roadmap
0.0 - Repository setup, using tiny-worker (because the original code is older than the worker_threads built into node.js)

0.1 - Using node's worker_threads and messages to route HTTP requests and responses between main thread and worker threads

0.2 - Basic web server functionality in main thread to serve simple requests without starting a worker-thread, e.g. deliver file content and cached HTTP responses

0.3 - Thread pool and intelligent routing HTTP requests to existing threads, e.g. depending on session cookie values so the same thread handles requests in a session

0.4 - Shared ACID key/value store supporting transactions

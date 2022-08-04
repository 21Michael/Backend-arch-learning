# One-way notifications

Implementing one-way notifications is straightforward using asynchronous messaging.
The client sends a message, typically a command message, to a point-to-point channel
owned by the service. The service subscribes to the channel and processes the mes-
sage. It doesn’t send back a reply.
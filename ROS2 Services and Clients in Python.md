ROS 2 Services (Request-Response)

Definition: ROS 2 service is a synchronous communication mechanism between nodes where a client sends a request and waits for a response from the server.

Purpose:

Execute on-demand actions (e.g., move robot arm)

Retrieve information once (e.g., sensor data)

Ensure client waits for the result before continuing

Components:

Service Server: Node that provides the service

Service Client: Node that calls the service

Request / Response: Data sent between client and server

Key Difference from Topics:

Topics = continuous streaming (asynchronous)

Services = single request-response (synchronous)

Example Use Case: Add two numbers, request robot position, start/stop simulation
Service Client → Request → Service Server → Response → Client

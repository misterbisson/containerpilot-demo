# containerpilot-single-random-backend

The purpose of this project is to demonstrate how to implement service discovery with [ContainerPilot](https://www.joyent.com/containerpilot). Specifically, this answers the question for how to connect each client service to _just one_ of a number of potential server (backend) services.

The use-case here is for an old client app that accepts a single DNS name or IP address in its configuration. This will demonstrate how to make that work, despite the limitations of the client.

This project is incomplete. The client app configuration will be written in an upcoming workshop.
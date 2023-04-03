<h1 align="center">
  <br>
  Ten Ten Platform Engineer Interview
  <br>
</h1>
<p align="center">
  <a href="https://tenten.app"><img src="./.assets/logo.png" alt="Ten Ten logo" width="120"></a>
</p>
<br>

## Test

The test consist in building a small distributed online-counter.

<p align="center">
  <img src="./.assets/diagram.svg" alt="Ten Ten logo" width="680">
</p>
<br>

It is split in 3 components:
- A "client"
- A "gateway"
- A "status" service

You need to build and package all three components.

To keep things simple, all the schemas are in a single protobuf file, but you're free to split it if you want.

### 1. The client

You need to write a gRPC client that:
- has a unique identifier
- connects to the gateway
- the gateway is going to send a `Ping` every 1s to the client.
- the client must respond with a `Pong`, containing a `Status` (cf `protos/service.proto`)

> You're free to write the `client` either in Go or Rust

### 2. The Gateway

You need to write a gRPC server that:
- allows multiple simultaneous clients to connect with persistent connections
- ping each connected client at a specific clockrate (a client must receive a `Ping` every 1s)
- the gateway must notify the `status` service
    - You're free to choose how the `gateway` talks to the `status` service (gRPC, event, ...)
- must be horizontally scalable
- Write a Dockerfile, as much production-ready as you can
- If any, point out scalability issues of your system / how you would fix them

> You're free to write the `gateway` either in Go or Rust

### 3. The Status service

You need to write a microservice that:

- can react to messages sent by the `gateway`
    - You're free to choose how the `gateway` talks to the `status` service (gRPC, event, ...)
- must expose a `StatusReader` gRPC service
- the service keeps track of how many **unique** users were online in the last 3mins
    - a user is considered online if they reported a `STATUS_EVEN` or `STATUS_ODD` status.
- must be resilient to reboots
    - you're free to use any kind of database you want
- must be horizontally scalable
- Write a Dockerfile, as much production-ready as you can
- If any, point out scalability issues of your system / how you would fix them

> You **must** write this service in Go

### 4. Demonstration

Finally, write a `docker-compose` to run all the services and allow for easy testing.

## If you've got extra time

- Write tests
- Add tracing instrumentation
- Build everything with Bazel:
    - Executables
    - Mutliplatform docker images

## Spontaneous applications

Interested in working with us? We're always looking for talents!

Shoot us an email at

<img src="./.assets/mail-dark.png#gh-dark-mode-only" alt="Email" width="100"/>
<img src="./.assets/mail-light.png#gh-light-mode-only" alt="Email" width="100"/>


<h3 align="center">
  <br>
  <hr>
    *Kkrshhtzz*
  <br>
    Over! ✌️
</h3>
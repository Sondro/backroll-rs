# backroll-rs

Backroll is a pure Rust implementation of [GGPO](https://www.ggpo.net/)
rollback networking library.

## Development Status
This is still a heavy WIP. At time of writing, this very much is a direct port of
GGPO's code from C++ to Rust. The API is subject to signifgant change in the
future.

## Differences with the C++ implementation

 * (Almost) 100% pure **safe** Rust. No unsafe pointer manipulation.
 * Type safety. backroll-rs heavily utilizes generics to allow for
 * Abstracted transport layer protocols - integrate and use any transport layer
   library you need. Comes with a raw UDP socket based implementation.
 * Configurable at compile time - Almost all Backroll types takes a
   `BackrollConfig` generic type parameter that specifies session constants.
   Does not require forking to change the hardcoded constants.
 * Reduced memory usage - Backroll's use of generics potentially shrinks down
   the sizes of many data types.
 * Vectorized input compression scheme - Backroll utilizes the same XOR + RLE
   encoding, but it's written to maximize CPU utilization.

## Planned features

 * Thread-safety - the transport layer abstractions. Currently the main data
   structures are not `Sync` nor `Send`.
 * Rust game engine integrations (bevy, amethyst, Piston, etc).

## Repository Structure

This repo contains the following crates:

 * backroll - the main Backroll interface, intended to be used as the original
   GGPO. (Partially complete)
 * backroll\_transport - An isolated set of transport layer abstractions. (In
   progress)
 * backroll\_transport\_udp - A transport layer implementation using raw UDP
   sockets. (Not started)
 * bevy\_backroll - a integration plugin for [bevy](https://bevyengine.org/).
   (Not started).

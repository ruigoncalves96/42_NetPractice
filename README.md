*This project has been created as part of the 42 curriculum by randrade.*

# NetPractice

*Rank 04 — TCP/IP addressing, by way of ten broken networks.*

## Description

NetPractice is the odd one out in the Common Core: there is nothing to compile and no
code to write. It is a networking exercise delivered as a small offline web app. Each of
its ten levels shows a diagram — hosts, switches, routers, and the interfaces between
them — with some IP addresses and routing table entries left blank or deliberately
wrong. Each level states one or more objectives at the top of the page; the job is to
adjust the unshaded fields until the network satisfies them.

The goal is to understand how **TCP/IP addressing** actually works, and the exercise
teaches it by breaking it:

- **Subnet masks and network boundaries.** Two hosts can only talk directly if they land
  in the same subnet. The mask decides where that boundary falls, and a mask one bit too
  wide silently merges two networks that were meant to stay apart.
- **Reserved addresses.** The all-zeroes host part is the network address and the
  all-ones is the broadcast address; neither can be assigned to an interface.
- **Default gateways and routing.** Once two hosts sit in different subnets, traffic
  needs a router, and the router needs to know where to forward it — via a default route
  or a specific destination entry.
- **Switches versus routers.** A switch forwards inside one network and has no address of
  its own; a router joins networks and needs an interface, correctly addressed, in each.

The later levels stop being fill-in-the-blank and become genuinely constrained: several
interfaces, limited address ranges, and routing tables where a single wrong mask makes an
otherwise valid configuration unreachable. A log panel at the bottom of the page explains
*why* a configuration fails — a missing gateway, an invalid address — which is the main
debugging tool.

## Instructions

### Running the training interface

The interface **must be served over HTTP** — browser security rules prevent it from
working when the pages are opened directly from the filesystem. The archive distributed
with the project includes a `run.sh` that starts a local web server and opens your
browser at the right page:

```sh
./run.sh
```

If `run.sh` does not work, serve the folder manually and browse to it:

```sh
cd net_practice && python3 -m http.server 49242
```

Then open **http://localhost:49242** (any free port will do).

### Using it

- **Enter your login** in the field on the front page so the interface generates *your*
  personal configuration. This matters — the submitted files are tied to it.
- The **evaluation** tab generates a random configuration instead, which is what is used
  during a defence.
- Work through `level1` … `level10`. Use **[Check again]** to validate the current
  configuration, and read the logs at the bottom when it fails.
- A button to advance appears once a level is solved.

### Exporting your configuration

On each level, press **[Get my config]** to download that level's configuration **before
moving on**. This is the deliverable — the exported files, not the web app.

### Submission

**Ten exported configuration files — one per level — must be placed at the root of the
Git repository.** Enter your login in the interface before exporting; the files are tied
to it.

At the defence you must solve **three randomly chosen levels** within a limited time, with
no external tools. A simple calculator such as `bc` is tolerated, and that is the limit —
so the addressing arithmetic has to be understood, not looked up.

> **Status of this repository:** the ten exported configuration files are **not present**
> here — only the training interface is checked in. They need to be exported from the
> interface and committed to the repository root before this project is submission-ready.

## Project structure

```
NetPractice/
├── README.md
└── net_practice/
    ├── index.html          # front page: login / evaluation tabs
    ├── level1..10.html     # the ten exercises
    ├── end.html            # completion page
    ├── js/                 # per-level definitions plus the simulator (sim.js, show.js)
    ├── css/                # styling
    ├── img/                # host, switch, router and internet icons
    └── License
```

The ten exported `.json` configuration files belong at the root, alongside `README.md`.

## Resources

### Networking concepts studied

- **TCP/IP addressing** — how an IPv4 address is split into a network part and a host
  part, and why that split is what decides reachability
- **Subnet masks** — dotted-decimal and CIDR prefix notation, and how the mask sets the
  network boundary
- **Reserved addresses** — network address and broadcast address, and why neither can be
  assigned to an interface
- **Default gateways** — how a host reaches anything outside its own subnet
- **Routers and switches** — routers join networks and hold an address per interface;
  switches forward within a single network and hold none
- **Routing tables** — destination and next-hop entries, and default routes
- **OSI layers** — where addressing (layer 3) sits relative to switching (layer 2)
- **Private address ranges** — the blocks reserved for internal use

### References

- [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918) — private address allocation
- [RFC 791](https://datatracker.ietf.org/doc/html/rfc791) — the Internet Protocol
- [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) — masks and prefixes
- [Subnetwork](https://en.wikipedia.org/wiki/Subnetwork) — subnetting explained
- [OSI model](https://en.wikipedia.org/wiki/OSI_model)
- [`netPractice.pdf`](../../../../Subjects/Rank_4/netPractice.pdf) — the project subject

### Use of AI

<!-- TODO (randrade): the subject requires this section to state which tasks and which
     parts of the project AI was used for. Replace this block with your own account —
     for example whether AI was used to explain subnetting concepts, to check address
     arithmetic, or not at all while solving the levels. -->

AI was used to draft and structure this README. The networking exercises themselves are
solved in the training interface, and at the defence three random levels must be solved
unaided — so any conceptual help has to translate into understanding that survives
without tools.

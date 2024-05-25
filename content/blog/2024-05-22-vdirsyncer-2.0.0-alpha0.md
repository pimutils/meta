---
layout: post
title: Vdirsyncer 2.0.0-alpha0 release notes
date: 2024-05-22
categories: blog
params:
  author: WhyNotHugo
---

I've just tagged a first alpha version of the vdirsyncer rewrite. This is an
EXPERIMENTAL VERSION, and has several missing features. It likely has bugs too,
so I appreciate anyone willing to test this and report bugs.

Keep in mind that as an early version, this MAY have bugs that result in data
loss. Ensure that you keep frequent backups. If you are unwilling to help report
bugs, please wait for a stable release.

Compared to the previous series, there are a few exciting changes.

## Continuing on errors

When synchronising a collection, if a single items fails, synchronisation will
continue and other items will be processed properly. This has an impact when a
server rejects a single calendar event, but I want the other 500 events in my
calendar to synchronise properly.

## Daemon

A new `daemon` command has been implemented. This keeps vdirsyncer running and
performing new synchronisations every five minutes[^minutes]. In future
releases, I intend to implement storage monitoring, so instead of having a fixed
timeout, synchronisations will be triggered only when a storage reports that
changes have occurred.

[^minutes]: This period is actually configurable.

I have been running `vdirsyncer daemon` in the background for the last few weeks
and am quite happy with the results.

## Collection creation and deletion

When a collection is created or deleted on one side, this change will
immediately replicate to the other side (assuming that the affected collections
match the current configuration).

This means that I can create a new calendar on one device, and it automatically
shows up on another.

If this behaviour is problematic for some use case, please do reach out so we
can find a solution.

## No more `discover`

The `discover` command is gone and no longer necessary; discovery of collections
is handled automatically.

## Conflict resolution

Conflict resolution is not executed during normal synchronisations. This is
mostly because there commands are usually interactive and would interrupt the
automated flow or regular synchronisations.

Use `vdirsyncer resolve-conflicts` to manually resolve any conflicts.

## Testing

Testers are welcome. Using a custom CA certificate and specifying TLS
certificate fingerprints has had minimal testing, so I would appreciate
real-world testing of this.

When migrating from the previous vdirsyncer implementation, ensure that your
collections are already in sync. A new, separate status file is used, so any
changes on either side will result in conflicts.

It is not trivial to migrate back to the previous version either: you will have
to ensure that both sides of your collection are in sync before doing so too.

# Installation

The current version needs to be built from source. The result is a single
binary, that can be copied onto other hosts without any additional support files
(note that binaries will only work across hosts of the same distribution and CPU
architecture).

```sh
curl -LO https://git.sr.ht/~whynothugo/vdirsyncer-rs/archive/vdirsyncer/v2.0.0-alpha0.tar.gz
tar xf v2.0.0-alpha0.tar.gz
cd vdirsyncer-rs-vdirsyncer/v2.0.0-alpha0
cargo build --release -p vdirsyncer
cp target/release/vdirsyncer /usr/local/bin/
```

Replace `/usr/local/bin/` with any other directory in `$PATH`.

Compilation will take a long time (several minutes, at least). I hope to improve
this in future releases, although Rust doesn't make this easy. Fortunately, this
cost pays off with vdirsyncer itself being quite lightweight at runtime.

# Feedback

See the [migration guide] for details on how to update a configuration file.
There is currently no documentation on setting up a new configuration from
scratch (this will be addressed at some point on a later release).

Please [join us on IRC][contact] if you have feedback or questions.

Issues are tracked in [a separate issue tracker][issues], to avoid any confusion
with existing issues from the previous implementation.

[contact]: /contact/
[issues]: https://todo.sr.ht/~whynothugo/vdirsyncer-rs

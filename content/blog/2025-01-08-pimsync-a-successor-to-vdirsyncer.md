---
layout: post
title: "pimsync: a successor to vdirsyncer"
date: 2025-01-08
categories: blog
params:
  author: WhyNotHugo
---

I previously posted about alpha and beta releases of the upcoming vdirsyncer
rewrite. My intention was to call this re-implementation "vdirsyncer v2".

I have since renamed this rewrite to `pimsync`. The main reasons for renaming
are to better disambiguate between the previous project and this project,
especially when in the context of issues, tutorials, and discussions in general.

# Which one to choose

`pimsync` is still missing some features from `vdirsyncer`, so the former is not
yet deprecated. Users relying on features that haven't been ported there should
use `vdirsyncer`. Otherwise, it is recommended to use `pimsync` instead.

Features missing from pimsync that were present in vdirsyncer are covered in
[the migration guide](https://pimsync.whynothugo.nl/pimsync-migration.7.html).

Pimsync's main advantages are:

- If synchronising a single item fails, it is skipped and `pimsync` continues
  to process all other items. `vdirsyncer` aborts the rest of operation.
- A new `daemon` command runs `pimsync` continuously in background, keeping
  calendars and address books in sync. Currently it relies on polling the
  storages, but work is ongoing to react to events instead.
- `pimsync` can automatically create new collections without any intervention.
- Dry runs are now possible. These allow inspecting which actions `pimsync`
  would take without making any changes.
- A lot of edge cases with regards to URL encoding are better handled.

There are a lot of corner cases which `vdirsyncer` won't handle well but were
kept in mind from the start for `pimsync`. Efforts are currently focused on the
latter, and the former shall be deprecated eventually (once all key features
have been ported).

# Following development

I post mostly status updates on [my personal blog][blog], which include more
insight into the development process for this and other projects. For those
only interested in new releases, I intend to continue publishing release notes
here.

[blog]: https://whynothugo.nl/

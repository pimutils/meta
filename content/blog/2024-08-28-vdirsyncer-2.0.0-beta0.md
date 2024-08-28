---
layout: post
title: Vdirsyncer 2.0.0-beta0 release
date: 2024-08-28
categories: blog
params:
  author: WhyNotHugo
---

I've tagged a beta release of the vdirsyncer v2. I believe that most usages that
can lead to data loss have been properly addressed. By tagging this beta, I
expect to gather from feedback from usage by others.

As always, please do back up your data, especially during the initial
configuration.

## Documentation

The biggest flaw right now is a strong lack of documentation. A [migration
guide] is still available for users of v1, but nothing else. I understand that
the lack of documentation is the main hindrance for adoption, even for early
testers, so documentation will be my main focus in the upcoming weeks and the
main target for the next beta.

[migration guide]:
  https://git.sr.ht/~whynothugo/vdirsyncer-rs/tree/v2.0.0-beta0/item/docs/content/docs/migration-guide.md

# Installation

The current beta needs to be built from source.

```sh
curl -LO https://git.sr.ht/~whynothugo/vdirsyncer-rs/archive/v2.0.0-beta0.tar.gz
tar xf v2.0.0-beta0.tar.gz
cd vdirsyncer-rs-v2.0.0-beta0/
make
doas make install
```

# Thanks

I'd like to extend my deep appreciation to NLnet for the grant we have received
that enabled my to work on vdirsyncer for so many hours. This effort would not
be possible without them. Thanks!

# Feedback

Please [join us on IRC][contact] if you have feedback or questions.

[contact]: /contact/

Issues are tracked in [a separate issue tracker][issues], to avoid any confusion
with existing issues from vdirsyncer v1.

[issues]: https://todo.sr.ht/~whynothugo/vdirsyncer-rs

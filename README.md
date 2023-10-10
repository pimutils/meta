# meta
Issue tracker for organizational matters and website

[![Build Status](https://travis-ci.org/pimutils/meta.svg?branch=master)](https://travis-ci.org/pimutils/meta)

## pimutils.org

The pimutils website is a [Lektor](https://www.getlektor.com/) project. After installing Lektor you should be able to run the admin interface using ``lektor server``. Pushing your changes to master will automatically deploy via Travis to GitHub pages.

The DNS is managed via Markus Unterwaditzer's (@untitaker) private accounts.

## Local usage

Create a virtual environment for lektor:

    mkvirtualenv pimutils-meta
    pip install -r requirements.txt

Build the project once with:

    lektor build --output-path ./build/

Or watch and rebuild when changes happen:

    fd | entr lektor build --output-path build

The built files can be served locally with just python:

    python -m http.server 6060 -d build

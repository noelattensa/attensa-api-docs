# Warning!  These docs are under heavy development!  Don't rely on this yet!

Attensa API documentation
========

This is the [Attensa](http://www.attensa.com) API documentation, based on the wonderful [Slate](https://github.com/tripit/slate)

Development
------------

### Requirements

 - **Linux or OS X** — Windows may work, but is unsupported.
 - **Ruby, version 1.9.3 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

 1. Clone this repository.
 2. Install all dependencies: `bundle install`
 3. Start the test server: `bundle exec middleman server`

Or use the included Dockerfile! (must install Docker first)

```shell
docker build -t slate .
docker run -d -p 4567:4567 slate
```

You can now see the docs at <http://localhost:4567>.

*Note: if you're using the Docker setup on OSX, the docs will be
availalable at the output of `boot2docker ip` instead of `localhost:4567`.*

You can learn what you need to know about editing [Slate](https://github.com/tripit/slate) markdown at their repo.

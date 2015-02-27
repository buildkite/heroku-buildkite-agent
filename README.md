# Sample buildkite-agent on Heroku

An example of running the buildkite-agent on a Heroku dyno using [Ø buildpack](https://github.com/ryandotsmith/null-buildpack) on their Cedar stack.

This embeds buildkite-agent version 1.0-beta.12.317 (Linux AMD64). To update the agent simply replace the `bin/buildkite-agent` and `etc/bootstrap.sh` with the [latest linux-amd64 release](https://github.com/buildkite/agent/releases). Pull requests welcome!

## Usage

```bash
# Create a dyno
heroku create my-buildkite-agent \
              --buildpack https://github.com/ryandotsmith/null-buildpack.git

# Put in your token and any metadata for targeting the agents
heroku config:set BUILDKITE_AGENT_TOKEN=xxx \
                  BUILDKITE_AGENT_META_DATA=key1=val2,key2=val2 \
                  BUILDKITE_BOOTSTRAP_SCRIPT_PATH=/app/etc/bootstrap.sh \
                  BUILDKITE_HOOKS_PATH=/app/hooks

# :rocket:
git push heroku master

# Spin up an agent on a 1x dyno
heroku scale agent=1

# Tail the logs
heroku logs -t

# Spin up an squadron of 2x agent dynos
heroku scale agent=24:2X
```

## Customising

You can fork this repo and add your own hooks via the hooks directory, or even switch it to a [multi-buildpack](https://github.com/ddollar/heroku-buildpack-multi) to you can make other tools available inside your dyno.

## Roadmap

* A heroku-buildpack-buildkite-agent, negating the need to embed the agent and the bootstrap.

## License

MIT

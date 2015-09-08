# buildkite-agent Heroku app

An example of running the buildkite-agent on a Heroku dyno using the [buildkite-agent build pack](https://github.com/buildkite/heroku-buildkite-agent-buildpack).

The agent will run with `heroku=true` metadata applied.

## Usage

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

Press the button above, provide your agent token, then hit "Deploy". Once it's
deployed, click on "Manage App" and scale up the `agent` process to at least 1.

You should see your Buildkite agent dashboard register the new agent.

To set it up on Heroku manually without the button, follow these instructions instead:

```bash
# Create a dyno
$ heroku create my-buildkite-agent \
               --buildpack https://github.com/buildkite/heroku-buildkite-agent-buildpack.git

# Put in your token and any metadata for targeting the agents
$ heroku config:set BUILDKITE_AGENT_TOKEN=xxx \
                    BUILDKITE_AGENT_META_DATA=key1=val2,key2=val2

# :rocket:
$ git push heroku master

# Spin up an agent on a 1x dyno
$ heroku scale agent=1

# Tail the logs
$ heroku logs -t

# Spin up an squadron of 2x agent dynos
$ heroku scale agent=24:2X
```

## Customising

You can fork this repo and add your own hooks into a directory specified by a `BUILDKITE_HOOKS_PATH` var you set.

## License

MIT

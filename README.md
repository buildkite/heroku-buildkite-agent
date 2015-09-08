# buildkite-agent Heroku app

An example of running the buildkite-agent on a Heroku dyno using the [buildkite-agent build pack](https://github.com/bjeanes/heroku-buildpack-buildkite-agent) on the Cedar stack.

## Usage

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

Press the button above, provide your agent token, then hit "Deploy". Once it's
deployed, click on "Manage App" and scale up the `agent` process to at least 1.

You should see your Buildkite agent dashboard register the new agent.

To set it up on Heroku manually without the button, follow these instructions instead:

```bash
# Create a dyno
$ heroku create my-buildkite-agent \
               --buildpack https://github.com/bjeanes/heroku-buildpack-buildkite-agent.git

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

You can fork this repo and add your own hooks via the hooks directory, or even switch it to a [multi-buildpack](https://github.com/ddollar/heroku-buildpack-multi) to you can make other tools available inside your dyno.

## License

MIT

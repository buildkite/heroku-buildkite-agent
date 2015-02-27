# buildkite-agent Heroku app

An example of running the buildkite-agent on a Heroku dyno using [Ø buildpack](https://github.com/ryandotsmith/null-buildpack) on their Cedar stack.

This embeds buildkite-agent version 1.0-beta.12.317 (Linux AMD64). To update the agent simply replace the `bin/buildkite-agent` and `etc/bootstrap.sh` with the [latest linux-amd64 release](https://github.com/buildkite/agent/releases). Pull requests welcome!

```
$ heroku logs -t
2015-02-27T03:23:43.210411+00:00 heroku[api]: Set BUILDKITE_AGENT_TOKEN, BUILDKITE_BOOTSTRAP_SCRIPT_PATH, BUILDKITE_HOOKS_PATH config vars by t@toolmantim.com
2015-02-27T03:24:09.990769+00:00 heroku[api]: Release v6 created by t@toolmantim.com
2015-02-27T03:24:09.990769+00:00 heroku[api]: Deploy 400a95c by t@toolmantim.com
2015-02-27T03:24:16.942876+00:00 heroku[api]: Scale to agent=1 by t@toolmantim.com
2015-02-27T03:24:18.878004+00:00 heroku[agent.1]: Starting process with command `bin/buildkite-agent start`
2015-02-27T03:24:20.746703+00:00 app[agent.1]:                 _._
2015-02-27T03:24:20.746721+00:00 app[agent.1]:            _.-``   ''-._
2015-02-27T03:24:20.746723+00:00 app[agent.1]:       _.-``             ''-._
2015-02-27T03:24:20.746725+00:00 app[agent.1]:   .-``                       ''-._      Buildkite Agent 1.0-beta.12.317
2015-02-27T03:24:20.746727+00:00 app[agent.1]:  |        _______________         |
2015-02-27T03:24:20.746729+00:00 app[agent.1]:  |      .'  ___________  '.       |     Name: 861e54f3-33bd-48d9-a255-0323e8edaf43
2015-02-27T03:24:20.746730+00:00 app[agent.1]:  |        .'  _______  '.         |     PID: 3
2015-02-27T03:24:20.746732+00:00 app[agent.1]:  |          .'  ___  '.           |
2015-02-27T03:24:20.746733+00:00 app[agent.1]:  |            .' | '.             |     https://buildkite.com/agent
2015-02-27T03:24:20.746735+00:00 app[agent.1]:  |               |                |
2015-02-27T03:24:20.746736+00:00 app[agent.1]:  |               |                |
2015-02-27T03:24:20.746739+00:00 app[agent.1]:   ``._           |            _.''
2015-02-27T03:24:20.746740+00:00 app[agent.1]:       `._        |         _.'
2015-02-27T03:24:20.746742+00:00 app[agent.1]:          `._     |      _.'
2015-02-27T03:24:20.746743+00:00 app[agent.1]:             ``. _|_ . ''
2015-02-27T03:24:20.746744+00:00 app[agent.1]: 
2015-02-27T03:24:20.756210+00:00 app[agent.1]: 2015-02-27 03:24:20 [INFO ] Registering Agent with Buildkite...
2015-02-27T03:24:20.969844+00:00 app[agent.1]: 2015-02-27 03:24:20 [INFO ] Agent successfully connected. Waiting for work...
2015-02-27T03:24:20.904909+00:00 app[agent.1]: 2015-02-27 03:24:20 [INFO ] Agent successfully registered
2015-02-27T03:24:20.904922+00:00 app[agent.1]: 2015-02-27 03:24:20 [INFO ] Connecting to Buildkite...
2015-02-27T03:24:19.555661+00:00 heroku[agent.1]: State changed from starting to up
```

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

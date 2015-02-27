# A sample buildkite-agent running on Heroku

```bash
$ heroku create my-buildkite-agent \
                --buildpack https://github.com/ryandotsmith/null-buildpack.git

$ heroku config:set BUILDKITE_AGENT_TOKEN=xxx \
                    BUILDKITE_AGENT_META_DATA=key1=val2,key2=val2 \
                    BUILDKITE_BOOTSTRAP_SCRIPT_PATH=/app/etc/bootstrap.sh \
                    BUILDKITE_HOOKS_PATH=/app/hooks

$ git push heroku master
```

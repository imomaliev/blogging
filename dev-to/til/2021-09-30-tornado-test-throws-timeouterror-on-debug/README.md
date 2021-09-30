# Tornado test throws: `TimeoutError` on debug

## Fix: `tornado.util.TimeoutError: Operation timed out after 5 seconds`

### Problem

Whenever I debug my test for tornado code in the end I get this error

```python
...
> raise TimeoutError('Operation timed out after %s seconds' % timeout)
E tornado.util.TimeoutError: Operation timed out after 5 seconds

.venv/lib/python3.7/site-packages/tornado/ioloop.py:575: TimeoutError
```

### Solution

This is due `ASYNC_TEST_TIMEOUT` environment variable
[From docs](https://www.tornadoweb.org/en/stable/testing.html#tornado.testing.AsyncTestCase.wait)

> In the event of a timeout, an exception will be thrown. The default timeout is 5 seconds; it may be overridden with a timeout keyword argument or globally with the `ASYNC_TEST_TIMEOUT` environment variable.

And could be fixed by setting this variable to a bigger value in seconds

```console
$ # running tests with ASYNC_TEST_TIMEOUT set to 10 minutes
$ ASYNC_TEST_TIMEOUT=600 python -m unittest
```

or if you are using `pytest` with `pytest-tornado` plugin by passing `--async-test-timeout` argument to `pytest` command

```console
$ pytest --async-test-timeout=600
```

### Links

-   https://www.tornadoweb.org/en/stable/testing.html#tornado.testing.AsyncTestCase.wait
-   https://stackoverflow.com/a/49149757/3627387

## Open same folder in another panel in mc

### Question

How to open same folder in another panel in [Midnight Commander](https://midnight-commander.org)?

### Answer

Use `Alt+i` or `Esc+i`. From man page

<!-- prettier-ignore -->
> Alt-i  make the current directory of the current panel also the current directory of the other panel. Put the other panel to the listing mode if needed.

### Links

-   https://midnight-commander.org
-   https://github.com/MidnightCommander/mc
-   https://unix.stackexchange.com/a/5926/172777

## Docker prune only unnamed volumes

### Question

I was trying to do some cleanup of space for docker and needed to prune my unnamed volumes names.

### Answer

Use `--filter` option. From docs:

> By default, all unused volumes are removed. You can limit the scope using
> the `--filter` flag. For instance, the following command only removes
> volumes which are not labelled with the `keep` label:
>
> ```console
> $ docker volume prune --filter "label!=keep"
> ```

But to create correct filter first we need to `inspect` volumes to find what labels and other parameters are present for them

```console
$ docker volume inspect project_volume
[
    {
        "CreatedAt": "2021-09-30T11:35:55Z",
        "Driver": "local",
        "Labels": {
            "com.docker.compose.project": "project",
            "com.docker.compose.version": "2.0.0",
            "com.docker.compose.volume": "project_volume"
        },
        "Mountpoint": "/var/lib/docker/volumes/project_project_data/_data",
        "Name": "project_project_data",
        "Options": null,
        "Scope": "local"
    }
]
```

So we could filter our volumes like this

```console
$ docker volume prune --filter 'label!=com.docker.compose.project'
```

**Note** `negative` filtering does not work for `docker volume ls` for some reason.

```console
$ docker volume ls --filter 'label!=com.docker.compose.project'
Error response from daemon: Invalid filter 'label!'
```

### Links

-   https://docs.docker.com/engine/reference/commandline/volume_inspect/
-   https://docs.docker.com/config/pruning/#prune-volumes

## Show only names of docker volumes

### Question

How to show only names of volumes

### Answer

Use `--format`.

```console
$ docker volume ls --format '{{.Name}}'
```

### Link

-   https://docs.docker.com/config/formatting/

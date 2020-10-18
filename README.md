# Go-Nodejs

This is a base golang and Node.js development image. It's based on the `golang:X.XX-alpineX.XX`image and extedned by the following applications:

*  bash
*  su-exec
*  tmux
*  make
*  git
*  nodejs
*  npm
*  watchexec

The image can be extended to start multiple _watch_ jobs in separate tmux windows.

## Example usage

Files can be foound in [example](https://github.com/xDevBase/go-nodejs/blob/master/example)

### Minimal Dockerfile

```
FROM xdevbase/go-nodejs:v1.14-v12

COPY ./overlay /
```
Execute: `docker build --tag app/develop:1.0 .`


### Examle folder structure
The `entrypoint` script will `source` all scrips in the folder `entrypoint.d` and bellow. The scrips just need a the bash shebang `#!/bin/bash`. The execution is ordered by `sort`.

```
|____overlay
| |____etc
| | |____entrypoint.d
| | | |____1-app
| | | | |____run
| | | |____2-sass
| | | | |____run
```

### Example run script

#### /etc/entrypoint.d/1-app/run

```bash
#!/bin/bash

tmux new-window -t "$SESSION_NAME:1" -n "server" \
    watchexec -e go -r -s SIGKILL go run .
```

#### /etc/entrypoint.d/2-sass/run

```bash
#!/bin/bash

tmux new-window -t "$SESSION_NAME:2" -n "sass" \
    npm run sass-watch
```

### Example docker run

```
docker run -it --rm \
		-v $(CURDIR):/go/src/github.com/app \
		-w /go/src/go/src/github.com/app \
		app/develop:1.0
```

![Example windows](https://github.com/xDevBase/go-nodejs/blob/master/example/example.png?raw=true)


## Versions
* [v1.14-v12](https://github.com/xDevBase/go-nodejs/blob/master/v1.14-v12) golang version 1.14 and Node.js version 12 available as `xdevbase/go-nodejs:v1.14-v12`

## Volumes

* None

## Ports

* None

## Available environment variables

```bash
GOPROXY = direct
```

## Contributing

Fork -> Patch -> Push -> Pull Request


## Authors

* [Thomas Harr](https://github.com/xdevthomas)


## License

MIT


## Copyright

```
Copyright © 2020 Thomas Harr <https://www.xdevcloud.de>
```
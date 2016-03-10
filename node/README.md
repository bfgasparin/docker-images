# Web Node.js Base Image

This image is a base imagem for Web node.js applications.

This image assumes your application uses [Bower][7] to manage packages.

![logo Nodejs](logo_nodejs.png)
![logo Bower](logo_bower.jpg)

[Nodejs][1]
[Bower][7]

## Supported tags and respective `Dockerfile` links

* [`web-0.10-onbuild` (*web-0.10-onbuild/Dockerfile*)][5]

This image variant [`web-0.10-onbuild`][5] is based on the official [`node:0.10-onbuild`][2]
image with some slight diferences.

# Supported tags and respective `Dockerfile` links

## Create a `Dockerfile` in your Node.js app project

    FROM node:web-0.10-onbuild
    # replace this with your application's default port
    EXPOSE 8888

You can then build and run the Docker image:

    docker build -t my-nodejs-app .
    docker run -it --rm --name my-running-app my-nodejs-app

This image includes multiple `ONBUILD` triggers which should cover most node applications.
The build will:

- `COPY package.json /usr/src/app/`
- `COPY .npmrc /usr/src/app/`
- `COPY bower.json /usr/src/app/`
- `COPY .bowerrc /usr/src/app/`
- `RUN npm install`
- `COPY . /usr/src/app`

The image assumes that your application:

- has a file named [`package.json`][3] listing its dependencies and defining its [start script][4].
- has a file named [`.npmrc`][9] configuring npm
- has a file named [`bower.json`][6] listing its dependencies
- has a file named [`.bowerrc`][10] configuring bower

### Notes

We copy `.bowerrc` and `bower.json` files to fix the lack of control over when the BUILD trigger
fires. Copying these files helps applications which uses [Bower][7] commands during a
[npm script][8].

For example, the following `package.json` that includes [Bower][7] as dependency and executes
`bower install` in the `postinstall` script will work for this image:

    {
      "name": "example package",
      "devDependencies": {
        "bower": "^1.3.1"
      },
      "scripts": {
        "postinstall": "bower install --allow-root"
      }
    }

About this issue, see [`docker/docker#5714`](https://github.com/docker/docker/issues/5714),
[`docker/docker#8240`](https://github.com/docker/docker/issues/8240),
[`docker/docker#11917`](https://github.com/docker/docker/issues/11917)).

## Troubleshooting

### Bower commands into package.json

If you run build commands as `root` user and you run bower commands during the `npm install`
command in your `package.json` file, you must disable bower interactive prompting. Add the
following configuration to your `.boweerrc` file:

    {
      "interactive": false
    }

You should also use the parameter `--allow-root` to you bower command. like the following
`package.json` file:

    {
      "name": "example",
      "scripts": {
        "postinstall": "bower install --allow-root",
      }
    }

or the build will not work.

### ǸPM scripts

If you run build commands as `root` user and you have scripts configured into you `package.json`
file, it will lead npm to fail, because npm tries to downgrade its privileges when it runs
scripts. To solve this problem, add the following line to your `.npmrc` file:

    unsafe-perm = true

[1]: https://nodejs.org/
[2]: https://registry.hub.docker.com/_/node/
[3]: https://docs.npmjs.com/files/package.json
[4]: https://docs.npmjs.com/misc/scripts#default-values
[5]: 0.10/onbuild/Dockerfile
[6]: http://bower.io/docs/creating-packages/#bowerjson
[7]: http://bower.io/
[8]: https://docs.npmjs.com/misc/scripts
[9]: https://docs.npmjs.com/files/npmrc
[10]: http://bower.io/docs/config/


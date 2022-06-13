# Redoc Cli Base Image

This image is a base imagem with a [Redoc Cli][1] binary to build [OpenAPI][2] definition documents.

# Supported tags and respective `Dockerfile` links

* [`0.13.16` (*0.13.16/Dockerfile*)](0.13.16/Dockerfile)

# How to use this image

Pull this image

```dockerfile
docker pull brunogasparin/redoc-cli:latest
```

Build a single HTML page from your yaml definitio file with:

```
docker run --rm -v $PWD:/build brunogasparin/redoc-cli:latest openapi.yaml
```

# Useful Links

- [Redoc Cli Oficial Image Repository][3]

[1]: https://redocly.com/docs/redoc/quickstart/
[2]: https://swagger.io/specification/
[3]: https://github.com/Redocly/redoc/blob/master/cli/README.md


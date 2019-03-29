# Jiskefet OpenAPI specification
This specification describes the Jiskefet REST API.
The spec was generated using the NestJS Swagger module.

## How to generate
1. Deploy the server using https://github.com/SoftwareForScience/jiskefet-deploy
2. Go to the spec endpoint, e.g. https://my.server.address/api/doc-json
3. Plug the output into https://editor.swagger.io/
4. Make some manual changes... see [Caveats]

## Caveats
### `isArray: false` bug
Due to a bug in the NestJS Swagger module, the generated spec contains some incorrect lines.
For more information: https://github.com/nestjs/swagger/pull/149

To fix it, run this command:
```
sed -i '/isArray: false/d' ./openapi-spec.yaml
```
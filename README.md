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

### Other errors
The NodeJS generation also contains errors due to incomplete/incorrect decorators in the back-end code.
The following are known issues:
 - Various numbers (such as IDs and counters) that should be specified as `type: integer` with `format: int64`,
   are instead specified as `type: number`, which is interpreted as a floating point by the client code generator.
 - Some parameters that should be int64s, are specified as strings (such as the pageSize, pageNumber and runNumber of `runs/get`)
 - Various user & auth related issues. The affected endpoints are currently not used by the C++/Go clients, fortunately.
   - Instead of an integer ID, `type: user` is specified, which is not a valid type.
   - The endpoint `/users/{id}/tokens` does not list a parameter for the ID, making it unusable.
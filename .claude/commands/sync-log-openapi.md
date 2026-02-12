Regenerate the OpenAPI 3.1 spec at `openapi/log.yaml` from the opendata log server source code.

## Steps

1. Read all server source files from `/Users/agavra/dev/opendata/log/src/server/`:
   - `http.rs` — route definitions (paths and HTTP methods)
   - `request.rs` — query parameter structs and request body parsing
   - `proto.rs` — protobuf/JSON message schemas (request and response types)
   - `error.rs` — error response format and HTTP status code mapping
   - `response.rs` — content type constants and response format negotiation

2. Extract from the source:
   - Routes: method, path, handler name
   - Query params: field name, type, required vs optional, doc comments
   - Request bodies: field names, types, serde rename rules (`camelCase`)
   - Response schemas: field names, types, serde rename rules (`camelCase`)
   - Error mapping: which `Error` variants map to which HTTP status codes

3. Regenerate `openapi/log.yaml` preserving this structure:
   - OpenAPI version: `3.1.0`
   - Query params use `snake_case` (serde Deserialize defaults)
   - JSON body/response fields use `camelCase` (`#[serde(rename_all = "camelCase")]`)
   - Bytes fields → `type: string, format: byte` (base64 in JSON)
   - Content type: `application/json`
   - Include examples derived from test cases in the source
   - Exclude operational endpoints (`/-/healthy`, `/-/ready`, `/metrics`)

4. Run `mint validate` in `/Users/agavra/dev/docs/` to verify the spec has no errors.

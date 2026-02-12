Regenerate the OpenAPI 3.1 spec for the given system from the opendata server source code.

**Usage:** `/sync-openapi <system> <opendata-repo-path>`

Example: `/sync-openapi log /Users/me/dev/opendata`

The arguments are: $ARGUMENTS

First, parse the arguments to extract the system name (first arg) and the path to the opendata repo (second arg). The system must be one of: `log`, `timeseries`. If either argument is missing, ask the user to provide it.

---

## System: log

**Source:** `<opendata-repo-path>/log/src/server/`
**Output:** `openapi/log.yaml`

### Steps

1. Read all server source files from `<opendata-repo-path>/log/src/server/`:
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

4. Run `npx @mintlify/cli validate` to verify the spec has no errors.

---

## System: timeseries

**Source:** `<opendata-repo-path>/timeseries/src/promql/`
**Output:** `openapi/timeseries.yaml`

### Steps

1. Read all server source files from `<opendata-repo-path>/timeseries/src/promql/`:
   - `server.rs` — route definitions, error mapping, handler functions
   - `request.rs` — query parameter structs and domain request types
   - `response.rs` — response schemas (Prometheus API format)
   - `remote_write.rs` — remote write protobuf types and handler

2. Extract from the source:
   - Routes: method, path, handler name (note: query/query_range/series support both GET and POST)
   - Query params: field name, type, required vs optional, serde rename rules (e.g. `match[]`)
   - Response schemas: field names, types, serde rename/skip annotations
   - Error mapping: `Error` variants → HTTP status codes and `errorType` strings
   - Remote write: content type requirements, protobuf schema, response codes

3. Regenerate `openapi/timeseries.yaml` preserving this structure:
   - OpenAPI version: `3.1.0`
   - Follows Prometheus HTTP API conventions
   - Document GET for dual-method endpoints; mention POST in descriptions
   - `match[]` parameters use `style: form, explode: true`
   - Timestamps accept RFC 3339 or Unix seconds (type: string)
   - Durations accept Prometheus format like `15s`, `1m` (type: string)
   - Error responses use `{ status, errorType, error }` format
   - Remote write endpoint documents protobuf + snappy content requirements
   - Exclude operational endpoints (`/-/healthy`, `/-/ready`, `/metrics`)

4. Run `npx @mintlify/cli validate` to verify the spec has no errors.

---
name: generate-ktor-client
description: Automatically generates a fully typed Ktor HTTP client for the Data layer.
---

# Generate Ktor Client Skill

Use this skill to quickly scaffold API integration code using Ktor in a Kotlin Multiplatform environment.

## Objectives
- Standardize network requests.
- Generate typed request/response models.
- Ensure proper error handling and coroutine usage.

## Step-by-Step Instructions

1. **Gather Requirements**:
   - Understand the API endpoint, HTTP method, and necessary headers or authentication.
   - If a schema (OpenAPI/Swagger) or JSON payload is provided, use it to generate Kotlin data classes.

2. **Generate Models**:
   - Inside `commonMain/.../data/models`, create internal data classes representing the API request and response bodies.
   - Annotate these classes with `@Serializable` (assuming `kotlinx.serialization` is used).

3. **Create the Client Service**:
   - Create a class or interface (e.g., `UserService.kt`) in the `data/network/` package.
   - Inject an instance of `HttpClient` into this service.
   - Write suspending functions for each endpoint.

4. **Implement Request Logic**:
   - Use the injected `HttpClient` to make requests (e.g., `client.get("...")`, `client.post("...")`).
   - Implement `try/catch` blocks or a `Result` wrapper to handle network exceptions (`IOException`, `SerializationException`).
   - Map the internal API models to Domain `Model`s before returning them to the Intent/Reducer layer.

5. **Finalize**:
   - Output the generated code and verify the structure adheres to the Separation of Concerns outlined in `GEMINI.md`.

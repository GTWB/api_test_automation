# API Test Cases – POST /posts

These test cases are designed for a typical REST endpoint:

`POST /posts`

with a request body like:

```json
{
  "title": "string",
  "body": "string",
  "userId": 1
}

Note: The tests are executed against JSONPlaceholder￼, which is a mock API.
It does not persist data or enforce validation strictly.
Where behaviour differs from a real production API, the “expected” behaviour is documented in the test case description.
```

# API Test Cases – POST /posts

This document describes a complete set of test cases for the REST endpoint:

`POST /posts`

### Expected Request Body

```json
{
  "title": "string",
  "body": "string",
  "userId": 1
}
```

> **Important:**  
> The tests are executed against **JSONPlaceholder**, a mock API used only for training purposes.  
> JSONPlaceholder does **not** persist data, does **not** validate fields strictly, and returns generic responses.  
> When the behaviour of JSONPlaceholder differs from a real production API, the _expected real‑world behaviour_ is explicitly documented.

---

# 1. Functional & Validation Test Cases

| TC_ID    | Area              | Description                                      | Preconditions          | Steps                                              | Expected Result (Real API)                                              |
| -------- | ----------------- | ------------------------------------------------ | ---------------------- | -------------------------------------------------- | ----------------------------------------------------------------------- |
| **TC01** | Happy path        | Create a post with valid title, body, and userId | Valid userId exists    | Send POST with valid JSON `{title, body, userId}`  | 201 Created; response includes id, title, body, userId; data persisted. |
| **TC02** | Required fields   | Missing `title`                                  | Valid userId exists    | Send POST without `title`                          | 400/422 error: “title is required”; no post created.                    |
| **TC03** | Required fields   | Missing `body`                                   | Valid userId exists    | Send POST without `body`                           | 400/422 error: “body is required”.                                      |
| **TC04** | Required fields   | Missing `userId`                                 | –                      | Send POST without `userId`                         | 400/422 error: “userId is required”.                                    |
| **TC05** | Type validation   | `userId` sent as string                          | –                      | Send POST with `"userId": "abc"`                   | 400/422 error: invalid type; no post created.                           |
| **TC06** | Type validation   | Empty title (`""`)                               | –                      | Send POST with empty title                         | 400/422 error: title cannot be empty.                                   |
| **TC07** | Length boundaries | Title exceeds maximum length                     | API defines max length | Send POST with overly long title                   | 400/422 error for exceeding allowed length.                             |
| **TC08** | Length boundaries | Body at maximum allowed length                   | Max length known       | Send POST where body is exactly the maximum length | 201 Created; accepted; no truncation or server error.                   |
| **TC09** | Referential check | Non-existent `userId`                            | userId does not exist  | Send POST with `userId = 99999`                    | 404 or 400/422: userId not found.                                       |
| **TC10** | Extra fields      | Unexpected fields in JSON                        | –                      | Send POST including unknown fields                 | API ignores unknown fields or returns structured validation error.      |
| **TC11** | Malformed JSON    | Broken JSON structure                            | –                      | Send POST with invalid JSON (missing brace/comma)  | 400 Bad Request; clear parsing error.                                   |

---

# 2. Authentication & Authorization Test Cases

_(JSONPlaceholder does not implement auth; expected results assume real environments.)_

| TC_ID    | Area           | Description                             | Preconditions               | Steps                                      | Expected Result (Real API)               |
| -------- | -------------- | --------------------------------------- | --------------------------- | ------------------------------------------ | ---------------------------------------- |
| **TC12** | Authentication | Missing authentication token            | API requires Bearer token   | Send POST without Authorization header     | 401 Unauthorized; token missing.         |
| **TC13** | Authentication | Invalid or expired token                | Token-based auth enabled    | Send POST with invalid token               | 401 Unauthorized; token invalid/expired. |
| **TC14** | Authorization  | User role not permitted to create posts | User has limited permission | Send POST as user with insufficient rights | 403 Forbidden: insufficient permissions. |

---

# 3. Data Consistency & Post‑Conditions

_(These apply only to real APIs with persistence; JSONPlaceholder cannot support them.)_

| TC_ID    | Area              | Description                              | Preconditions  | Steps                                   | Expected Result (Real API)                                       |
| -------- | ----------------- | ---------------------------------------- | -------------- | --------------------------------------- | ---------------------------------------------------------------- |
| **TC15** | Data persistence  | Verify the created post can be retrieved | TC01 passes    | POST → capture id → GET `/posts/{id}`   | GET returns same data as POST; 200 OK.                           |
| **TC16** | Data in list      | Verify post appears in list endpoints    | TC01 passes    | POST → GET `/posts` or `/posts?userId=` | Newly created post is visible in the list.                       |
| **TC17** | Idempotency check | Verify behaviour when POST is re‑sent    | Depends on API | Send identical POST twice               | Either two posts created or 409 Conflict, depending on API spec. |

---

# 4. Notes About JSONPlaceholder Behaviour

- It always returns `201 Created` on POST, even with invalid or missing fields.
- Data is **not stored**, so GET after POST does not return newly created objects.
- It does not enforce validation rules.
- This makes it suitable for **learning request/response mechanics**, not real validation.

Where applicable, the _expected_ behaviour sections describe how a correctly implemented API would respond.

---

# 5. Tools & Execution

- Postman for requests and automated tests
- Postman CLI / VS Code for local execution
- GitHub for version control and documentation

This document represents a professional, real‑world style API test suite, adapted for execution on a mock server but fully aligned with how QA Engineers design test coverage for REST endpoints.

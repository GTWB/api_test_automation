# 📘 API Test Automation – Training Project

This repository contains a complete **API testing mini-framework** built using **Postman**, designed as part of a QA Automation Engineering learning roadmap.  
It demonstrates the ability to:

- Design API test cases professionally
- Implement automated checks using Postman test scripts
- Run tests manually or via automation runners
- Document API behaviour clearly and accurately
- Work with mock APIs (JSONPlaceholder) while reasoning like a real API QA engineer

This project is structured exactly like a real-world QA automation portfolio piece.

---

## 🔧 Tools & Technologies

| Tool                                        | Purpose                                                    |
| ------------------------------------------- | ---------------------------------------------------------- |
| **Postman**                                 | Build requests, write assertions, automate checks          |
| **Postman Collection Runner / Postman CLI** | Execute the full test suite                                |
| **JSONPlaceholder**                         | Public mock REST API used for training                     |
| **GitHub**                                  | Version control, documentation, and portfolio presentation |
| **VS Code**                                 | Editing documentation and test scripts                     |

---

## 📂 Repository Structure

```
API Test Automation/
 ├── postman/
 │    ├── API_POSTS_collection.json
 │    └── API_Training_Env.postman_environment.json
 │
 ├── docs/
 │    └── api_test_cases_posts.md
 │
 └── README.md
```

---

## 🧪 What’s Being Tested

This project focuses on the REST endpoint:

`POST /posts`

Expected request body:

```json
{
  "title": "string",
  "body": "string",
  "userId": 1
}
```

Because JSONPlaceholder does **not** persist data or enforce validation, the suite includes:

- Happy-path tests
- Negative tests (missing fields, wrong types)
- Malformed JSON tests
- Documentation that explains expected real‑world behaviour

This shows understanding of **real API validation rules**, even when the mock API behaves differently.

---

## 🗂️ Documentation

All API test cases are documented in:

```
docs/api_test_cases_posts.md
```

This file includes:

- Full test case descriptions
- Preconditions & steps
- Expected results (mock API vs real APIs)
- Validation, error handling, boundaries, and security checks

---

## ▶️ Running the Test Suite

### **1. Run manually with Postman Collection Runner**

1. Open Postman
2. Import the collection from `postman/API_POSTS_collection.json`
3. Select environment (optional)
4. Run the collection
5. View pass/fail results

---

### **2. Run from the terminal using Postman CLI**

Install:

```bash
npm install -g postman-cli

```

Run:

```bash
postman collection run "postman/API_POSTS_collection.json" \
  -e "postman/API_Training_Env.postman_environment.json"
```

This makes the suite CI‑ready and demonstrates automation capability.

---

## 📌 Key Skills Demonstrated

- API test design (functional, negative, boundary, security)
- Postman automation using scripts (`pm.test`, assertions, JSON validation)
- Handling differences between real APIs and mock APIs
- GitHub project structure & documentation
- Building a portfolio-ready automation project

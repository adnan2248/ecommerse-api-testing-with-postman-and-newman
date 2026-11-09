# E-Commerce API Testing | Postman & Newman

## Project Overview

This project focuses on testing RESTful E-Commerce APIs using **Postman** for manual and automated API testing and **Newman** for command-line test execution and HTML reporting.

The project covers Product APIs, Authentication, Authorization, and Cart operations, including positive and negative test scenarios.

**API Platform:** [DummyJSON](https://dummyjson.com/)

## Tools & Technologies

- Postman – API testing and automation
- Newman – Command-line collection execution
- Newman HTML Extra Reporter – HTML test reporting
- JavaScript – Automated test scripts
- REST API – HTTP methods and response validation

## Project Features

### 1. Products API Testing
- Retrieve all products
- Retrieve products with a limit
- Retrieve a product by valid ID
- Validate invalid product IDs
- Validate response structure and product details

### 2. Authentication Testing
- Login with valid credentials
- Login with invalid credentials
- Retrieve authenticated user information
- Test requests without authentication
- Test invalid bearer tokens
- Validate access tokens and user information

### 3. Cart API Testing
- Retrieve all carts
- Retrieve cart by ID
- Create a new cart
- Update cart using PUT
- Update cart using PATCH
- Delete a cart
- Test invalid cart IDs
- Test empty product arrays
- Test negative product quantities

## HTTP Methods Covered

| Method | Purpose |
|---|---|
| GET | Retrieve products, users and carts |
| POST | Login and create carts |
| PUT | Update cart |
| PATCH | Partially update cart |
| DELETE | Delete cart |

## Automation & Reporting

Automated test scripts were written using Postman's JavaScript-based testing framework.

Newman was used to execute the exported Postman collection through the command line.

The Newman HTML Extra Reporter generates detailed HTML reports containing request results, response information, and assertion results.

### Newman Execution

```bash
npx newman run "collections/restfull ecommerz.postman_collection.json"
```

### HTML Report Generation

```bash
npx newman run "collections/restfull ecommerz.postman_collection.json" -r htmlextra --reporter-htmlextra-export "reports/ecommerce-api-report.html"
```

## Test Execution Summary

| Metric | Result |
|---|---:|
| Total API Requests | 19 |
| Test Scripts Executed | 19 |
| Total Assertions | 64 |
| Passed Assertions | 60 |
| Failed Assertions | 4 |
| Assertion Pass Rate | 93.75% |

**Execution Status:** Completed

## Defects & Observations

### BUG-001: Negative Product Quantity Accepted

- Endpoint: `POST /carts/add`
- Expected: API should reject negative quantities.
- Actual: API returned `201 Created` and accepted quantity `-5`.
- Result: Validation failure observed.

### BUG-002: Inconsistent Authentication Response

- Endpoint: `GET /auth/me`
- Expected: `401 Unauthorized` without a token.
- Actual: During full collection execution, the API returned `200 OK` without an Authorization header.
- Individual Newman execution returned `401 Unauthorized`.
- Result: Inconsistent behavior observed and documented.

**Note:** DummyJSON is a simulated API. These findings describe observed behavior on the test platform and are not confirmed production-system vulnerabilities.

## Skills Demonstrated

- REST API Testing
- Manual API Testing
- Postman Collections
- JavaScript Test Automation
- Positive and Negative Testing
- Authentication and Authorization Testing
- CRUD Operations
- HTTP Status Code Validation
- JSON Response Validation
- Newman CLI Execution
- HTML Test Reporting
- Bug Reporting and Documentation

## Project Structure

```text
E-Commerce-API-Testing/
│
├── collections/
│   └── restfull ecommerz.postman_collection.json
│
├── reports/
│   └── ecommerce-api-report.html
│
├── bug-reports/
│   └── E-Commerce-API-Bug-Reports.md
│
└── README.md
```

## How to Run This Project

**Prerequisites:**
- Node.js and npm
- Postman
- Newman
- Newman HTML Extra Reporter

**Install Newman and the reporter:**

```bash
npm install -g newman newman-reporter-htmlextra
```

**Execute the collection:**

```bash
npx newman run "collections/restfull ecommerz.postman_collection.json"
```

**Generate the HTML report:**

```bash
npx newman run "collections/restfull ecommerz.postman_collection.json" -r htmlextra --reporter-htmlextra-export "reports/ecommerce-api-report.html"
```

## Author

**Adnan Hossain**

Aspiring Software Quality Assurance Engineer

Interested in Manual Testing, API Testing, and Test Automation.


# Bug Report – E-Commerce API Testing

**Project:** E-Commerce REST API Testing  
**API Platform:** DummyJSON  
**Testing Tools:** Postman, Newman  
**Test Type:** Functional, Negative and API Validation Testing  
**Reported By:** Adnan Hossain  
**Date:** 09 November 2026

---

# BUG-001: API Accepts Negative Product Quantity

| Field | Details |
|---|---|
| Bug ID | BUG-001 |
| Module | Cart |
| Endpoint | POST /carts/add |
| Severity | Medium |
| Priority | High |
| Status | Failed – Observed |
| Test Case | TC-19 |

### Description
The API accepts a negative product quantity when creating a new cart instead of rejecting the invalid input.

### Preconditions
- API endpoint is accessible.
- Valid user ID and product ID are provided.

### Request Payload

```json
{
  "userId": 1,
  "products": [
    {
      "id": 1,
      "quantity": -5
    }
  ]
}
```

### Steps to Reproduce
1. Open Postman.
2. Select POST method.
3. Enter `https://dummyjson.com/carts/add`.
4. Select Body → raw → JSON.
5. Enter the negative quantity payload.
6. Send the request.
7. Observe the response.

### Expected Result
The API should reject negative quantities and return HTTP 400 Bad Request or 422 Unprocessable Content.

### Actual Result
- Status Code: 201 Created
- Returned Quantity: -5
- Negative quantity was accepted.

### Impact
An API that accepts negative quantities may allow invalid cart data and incorrect quantity calculations.

### Evidence
Newman execution:
- API should reject negative quantity – FAILED.
- Negative quantity should not be accepted – FAILED.

---

# BUG-002: Unauthenticated Request Returns HTTP 200

| Field | Details |
|---|---|
| Bug ID | BUG-002 |
| Module | Authentication |
| Endpoint | GET /auth/me |
| Severity | Medium |
| Priority | High |
| Status | Inconsistent Behavior Observed |
| Test Case | TC-8 |

### Description
The API returns HTTP 200 OK for an unauthenticated request during full Newman collection execution, even though the Authorization header is absent.

### Steps to Reproduce
1. Open Postman.
2. Select GET method.
3. Enter `https://dummyjson.com/auth/me`.
4. Set Authorization to No Auth.
5. Execute the request through Newman.
6. Observe the response.

### Expected Result
The API should return HTTP 401 Unauthorized when no valid authentication token is provided.

### Actual Result
During full collection execution:
- Authorization Header: Undefined.
- Status Code: 200 OK.
- Authenticated user information was returned.

During individual Newman execution:
- Status Code: 401 Unauthorized.
- All three assertions passed.

### Impact
The inconsistent behavior makes authentication validation unreliable and requires further investigation.

### Evidence
Full Newman execution:
- Status code is 401 – FAILED.
- Unauthorized error message exists – FAILED.

Individual Newman execution:
- Status code is 401 – PASSED.
- Response is valid JSON – PASSED.
- Unauthorized error message exists – PASSED.

---

# Overall Bug Summary

| Metric | Result |
|---|---:|
| Total reported findings | 2 |
| Cart validation findings | 1 |
| Authentication findings | 1 |
| Confirmed production defects | Not established |
| Testing tool | Postman + Newman |

**Note:** DummyJSON is a simulated API. These findings describe observed behavior in the test environment and should not be presented as confirmed vulnerabilities in a production e-commerce system.
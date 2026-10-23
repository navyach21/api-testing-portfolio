# Restful-Booker API Testing with Postman

## Project Overview

This project contains API test cases for the [Restful-Booker API](https://restful-booker.herokuapp.com/), created and executed using **Postman**. It demonstrates API testing fundamentals, including authentication, booking CRUD operations, response validation, and the use of environment variables to pass data between requests.

## Tools and Technologies

- **Postman** — API requests and test automation
- **JavaScript** — Postman test scripts using `pm.test()` and `pm.expect()`
- **REST API** — HTTP methods, request headers, JSON request/response bodies
- **Environment variables** — dynamic storage of the authentication token and booking ID

## Test Coverage

The collection is organized into two folders: `Auth` and `Booking CRUD`.

| Area | Request | Purpose | Key validations |
|---|---|---|---|
| Health check | `GET /ping` | Check API availability | Status `201`; response text `Created` |
| Create token | `POST /auth` | Obtain an authentication token | Status `200`; token is a non-empty string and is saved to `token` |
| Create booking | `POST /booking` | Create a booking | Status `200`; booking ID is a positive number; booking fields match expected values |
| Get booking | `GET /booking/{{bookingId}}` | Retrieve the created booking | Status `200`; booking details, field types, and expected response keys |
| Update booking | `PUT /booking/{{bookingId}}` | Replace booking details | Status `200`; updated last name and price are correct; other expected values remain unchanged |
| Partial update | `PATCH /booking/{{bookingId}}` | Update selected booking fields | Status `200`; updated first and last names are correct; other values remain unchanged |
| Delete booking | `DELETE /booking/{{bookingId}}` | Delete the booking | Status `201`; response text `Created` |
| Confirm deletion | `GET /booking/{{bookingId}}` | Verify the booking no longer exists | Status `404`; response contains `Not Found` |

## Test Data and Assertions

The collection uses the following booking data during creation:

```json
{
  "firstname": "Navya",
  "lastname": "C H",
  "totalprice": 5000,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-11-01",
    "checkout": "2026-11-05"
  },
  "additionalneeds": "Breakfast"
}
```

The update request changes `lastname` to `Shree` and `totalprice` to `7000`. The partial update then changes `firstname` to `Allen` and `lastname` to `George`.

Assertions in the collection validate:
- HTTP status codes and response messages
- Presence and validity of the booking ID
- Expected booking field values
- JSON field data types
- The expected set of response keys
- Preservation of fields not changed by an update
- Successful deletion and subsequent `404 Not Found`

## Environment Configuration

The exported Postman environment defines these variables:

| Variable | Purpose |
|---|---|
| `baseUrl` | Base URL for API requests |
| `token` | Authentication token returned by `POST /auth` |
| `bookingId` | ID returned by `POST /booking` |

The uploaded environment export has empty values for these variables. Set `baseUrl` to:

```text
https://restful-booker.herokuapp.com
```

The test scripts are designed to populate `token` and `bookingId` dynamically when the relevant requests run.

## How to Run the Tests

1. Clone or download this repository.
2. Open Postman.
3. Import `Restful-Booker API Tests.postman_collection.json`.
4. Import `Restful-Booker.postman_environment.json`.
5. Select the **Restful-Booker** environment.
6. Set the `baseUrl` environment variable to `https://restful-booker.herokuapp.com`.
7. Run the requests in sequence:
   1. `Health check (ping)`
   2. `Create Token`
   3. `Create booking`
   4. `Get booking`
   5. `Update booking(PUT)`
   6. `Partial update(PATCH)`
   7. `Delete Booking`
   8. `Confirming Deletion`
8. Review the **Test Results** tab for each request, or run the collection in the Collection Runner and review its results.

**Important:** Run the requests in sequence because the collection stores the token and booking ID for later requests. The deletion confirmation is expected to return `404` after deletion. The public demo API may be reset or behave differently at times, so verify actual results when executing the collection.

## Screenshots

Add your Postman result screenshots to a folder named `screenshots/` in this repository. Replace the example filenames below with your actual image filenames.

### Collection Run Summary

![Postman collection run summary](screenshots/collection-run-summary.png)

### Authentication Tests

![Authentication test results](screenshots/auth-test-results.png)

### Booking CRUD Tests

![Booking CRUD test results](screenshots/booking-crud-results.png)

### Deletion Verification

![Deletion verification test results](screenshots/deletion-verification.png)

> If you have only one screenshot, keep the relevant section and remove the others. Make sure the image filenames and paths match the files committed to the repository.

## Project Structure

```text
Restful-Booker-API-Testing/
├── Restful-Booker API Tests.postman_collection.json
├── Restful-Booker.postman_environment.json
├── README.md
└── screenshots/
    ├── collection-run-summary.png
    ├── auth-test-results.png
    ├── booking-crud-results.png
    └── deletion-verification.png
```

## Skills Demonstrated

- REST API testing with Postman
- Writing automated assertions in JavaScript
- Validating HTTP status codes and JSON responses
- Testing POST, GET, PUT, PATCH, and DELETE methods
- Using environment variables for reusable and chained requests
- Verifying full and partial updates
- Validating negative scenarios after resource deletion
- Organizing API tests into collection folders

## Notes

- This is a practice project using the public Restful-Booker demo API.
- The README documents the test scripts in the exported collection; it does not claim a pass rate or successful execution without verified run results.
- Keep real credentials and sensitive tokens out of public repositories. The sample credentials in a practice collection should not be reused for real services.

## Author

**Navya C H**

API Testing | Postman | JavaScript Assertions

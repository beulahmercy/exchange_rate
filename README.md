Here's a detailed `README.md` template for your Spring Boot application:

---

# Currency Exchange and Discount Calculation API

## Description

This Spring Boot application integrates with a third-party currency exchange API to retrieve real-time exchange rates and calculate the total payable amount for a bill in a specified currency. It applies discounts based on user roles and other criteria. The API is secured with Basic Authentication.

---

## Features

1. **Third-Party API Integration**:
    - Fetches real-time exchange rates using the ExchangeRate-API.
2. **Discount Calculation**:
    - Employee: 30% discount (excluding groceries).
    - Affiliate: 10% discount (excluding groceries).
    - Long-term customer (2+ years): 5% discount (excluding groceries).
    - Additional $5 discount for every $100 on the bill.
3. **Currency Conversion**:
    - Converts the bill amount from the original currency to the target currency.
4. **Authentication**:
    - Secured API endpoints using Basic Authentication.

---

## Prerequisites

1. **Java**: Version 17 or higher.
2. **Gradle**: Installed on your machine or use the Gradle wrapper (`./gradlew`).
3. **ExchangeRate-API Key**:
    - Sign up at [ExchangeRate-API](https://open.er-api.com/) to get an API key.

---

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Update the `application.properties` with your ExchangeRate-API key:
   ```yaml
   currency:
     api:
       key: your-api-key
   ```

3. Build the project:
   ```bash
   ./gradlew build
   ```

4. Run the application:
   ```bash
   ./gradlew bootRun
   ```

5. Access the API at:
    - `http://localhost:8080/api/calculate?targetCurrency=EUR`

---

## API Endpoint Details

### **POST /api/calculate**

**Description**: Accepts bill details and calculates the final payable amount in the target currency.

**Request Body**:
```json
{
  "user": {
    "type": "employee",
    "tenureInYears": 1
  },
  "totalAmount": 150,
  "category": "electronics",
  "currency": "USD"
}
```

**Response**:
```string
96.009
```

**Authentication**:
- Basic Authentication is required.
- Default credentials:
    - Username: `user`
    - Password: `password`

---

## Testing Steps

1. Run the tests:
   ```bash
   ./gradlew test
   ```

2. View the test reports:
    - Navigate to `build/reports/tests/test/index.html` to view detailed test results.

---

## Code Coverage

1. Run the tests with coverage:
   ```bash
   ./gradlew jacocoTestReport
   ```

2. View the coverage report:
    - Open `build/reports/jacoco/test/html/index.html` in a browser.

---

## Static Code Analysis (Optional)

To ensure code quality, run static code analysis using SpotBugs:
```bash
./gradlew check
```
The report will be generated under `build/reports/spotbugs`.

---

## Additional Notes

1. **Caching**:
    - Exchange rates are cached for 1 hour to reduce API calls.
2. **Future Enhancements**:
    - Support for additional discount rules.
    - Integration with more third-party currency APIs.

---

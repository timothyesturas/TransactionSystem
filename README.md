# Transaction Management System

A full-stack web application for viewing and adding financial transactions. Built with Angular and Spring Boot, the application displays transaction summaries, manages transaction records, and stores data in a CSV file without requiring a database.

## 1. Technology Stack

| Component | Technology |
|---|---|
| Frontend | Angular 21, TypeScript 5.9 |
| UI Framework | Bootstrap 5.3 |
| Backend | Java 17, Spring Boot 4.1.2 |
| Build Tool | Maven |
| CSV Processing | Apache Commons CSV |
| Frontend Testing | Vitest |
| Data Storage | CSV File |

## 2. Project Structure

```text
transaction-management/
├── transaction-frontend/
│   ├── src/app/
│   │   ├── models/
│   │   ├── services/
│   │   └── pages/transactions/
│   ├── package.json
│   └── angular.json
│
├── transaction-backend/
│   ├── src/main/java/
│   │   └── com/example/transaction_backend/
│   │       ├── controller/
│   │       ├── service/
│   │       ├── repository/
│   │       ├── model/
│   │       └── dto/
│   ├── src/main/resources/
│   ├── data/transactions.csv
│   └── pom.xml
│
└── README.md
```

## 3. Prerequisites

Install the following before running the application:

| Software | Required Version |
|---|---|
| Git | Recent version |
| Node.js | 20.19+, 22.12+, or 24+ |
| npm | 10+ |
| JDK | 17 or newer |
| Maven | 3.9+ (optional; Maven Wrapper included) |

## 4. Installation

**Step 1: Clone the repository**

```bash
git clone <REPOSITORY_URL>
cd transaction-management
```

**Step 2: Install backend dependencies**

```bash
cd transaction-backend
```

Windows:

```powershell
.\mvnw.cmd clean install
```

macOS/Linux:

```bash
./mvnw clean install
```

**Step 3: Install frontend dependencies**

```bash
cd ../transaction-frontend
npm install
```

## 5. Configuration

**Backend:** `transaction-backend/src/main/resources/application.properties`

| Property | Default |
|---|---|
| `spring.application.name` | `transaction-backend` |
| `server.port` | `8081` |
| `app.csv.file` | `./data/transactions.csv` |

The backend stores transactions in `data/transactions.csv`. The file and its parent directory are created automatically if they do not exist.

**Frontend:** `transaction-frontend/src/app/services/transaction.ts`

Configure the backend API URL:

```typescript
private readonly apiUrl = 'http://localhost:8081/transactions';
```

The backend allows frontend requests from `localhost:4200` and `localhost:4201`. Update the `@CrossOrigin` configuration in `TransactionController.java` if using another origin.

## 6. Running the Application

Start the backend first. Run each application in a separate terminal.

**Terminal 1 — Backend**

```bash
cd transaction-backend
```

Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

macOS/Linux:

```bash
./mvnw spring-boot:run
```

**Terminal 2 — Frontend**

```bash
cd transaction-frontend
npm start
```

Open the application:

- Frontend: http://localhost:4200
- Backend API: http://localhost:8081/transactions

To stop either application, press `CTRL + C` in its terminal.

## 7. Application Features

- View all financial transactions.
- Display total, settled, pending, and failed transaction counts.
- Add transactions through a form.
- Validate required fields and transaction amounts.
- Automatically assign transaction statuses through the backend.
- Persist transaction records in a CSV file.
- Display success and error messages.

**Transaction Fields:**

| Field | Validation |
|---|---|
| Transaction Date | Required; defaults to today |
| Account Number | Required |
| Account Holder Name | Required |
| Amount | Required; minimum `0.01` |
| Status | Automatically assigned by the backend |

## 8. API Documentation

**Base URL:** `http://localhost:8081`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/transactions` | Retrieve all transactions |
| POST | `/transactions` | Add a new transaction |

**POST Request Body:**

```json
{
  "transactionDate": "2025-03-11",
  "accountNumber": "1111-2222-3333",
  "accountHolderName": "Test User",
  "amount": 42.50
}
```

**Successful Response: `201 Created`**

```json
{
  "transactionDate": "2025-03-11",
  "accountNumber": "1111-2222-3333",
  "accountHolderName": "Test User",
  "amount": 42.50,
  "status": "Pending"
}
```

The backend assigns the status automatically (`Pending`, `Settled`, or `Failed`).

For detailed request and response testing, use Postman or curl.

## 9. Testing

**Backend tests:**

```bash
mvn test
```

Or use the Maven Wrapper:

```bash
./mvnw test
```

**Frontend tests:**

```bash
npm test
```

**Manual testing:**

1. Start both applications.
2. Verify that existing transactions load.
3. Test form validation using empty fields and invalid amounts.
4. Add a transaction and verify its assigned status.
5. Refresh the browser and confirm that the transaction persists.
6. Stop the backend and verify that the frontend displays an error.

**Note:** Some existing frontend scaffold tests require updates before the test suite can pass. See the individual test files for details.

## 10. Troubleshooting

| Problem | Solution |
|---|---|
| `npm` or `node` not recognized | Install Node.js and configure PATH. |
| `mvn` not recognized | Use the included Maven Wrapper. |
| Port 4200 already in use | Run `npx ng serve --port 4201`. |
| Port 8081 already in use | Stop the conflicting process or change the backend port. |
| Unable to retrieve transactions | Ensure the backend is running and the API URL is correct. |
| CORS error | Update `@CrossOrigin` in `TransactionController.java`. |
| API returns 500 | Check `data/transactions.csv` for blank rows, invalid dates, or malformed records. |

---

**Quick Start**

| Component | Command |
|---|---|
| Backend | `mvn spring-boot:run` |
| Frontend | `npm start` |
| Backend API | `http://localhost:8081/transactions` |
| Application | `http://localhost:4200` |

**Note:** Start the backend before the frontend.

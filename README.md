# AMC Bank - 
## Stack
- Java 17, Spring Boot 3.3.4
- Spring Web, Spring Data JPA, Spring Security
- PostgreSQL
- JJWT 0.12.6
- React + Vite

## Final capabilities
- Admin/customer login with JWT
- ROLE_ADMIN and ROLE_CUSTOMER authorization
- Admin dashboard and customer CRUD
- Customer search
- Accounts: open, list, deposit, withdraw
- Loans: list and sanction with eligibility rules + EMI
- Customer self-service: profile, own accounts, own loans, deposit, withdraw, change password
- BCrypt password hashing
- Account ownership checks
- React Bearer-token integration

## 1. PostgreSQL
Start PostgreSQL and run:

```sql
CREATE DATABASE amc_bank_customer_login;
```

Default classroom configuration expects user `postgres`, password `1234` in my computer, port `5432`. Change `backend/src/main/resources/application.properties` based on settings in your computer

## 2. Backend in Eclipse
1. File > Import > Maven > Existing Maven Projects.
2. Select the `backend` folder.
3. Finish.
4. Right-click project > Maven > Update Project if dependencies are still downloading.
5. Run `AmcBankApplication.java` as Spring Boot App.
6. Backend runs at http://localhost:8080.

Demo admin login: `admin` / `admin123`.
Admin demo: admin / admin123
Customer: use the email and first password created by the admin.
## 3. Frontend in VS Code
Open the `frontend` folder, then:

```bash
npm install
npm run dev
```

Open the Vite URL, normally http://localhost:5173.

## 4. Final learning flow
Login -> JWT -> React stores token -> Bearer token -> Spring Security filter -> role authorization -> controller -> service -> JPA -> PostgreSQL.

## 5. Important API groups
Public: POST /api/login
Authenticated: GET /api/auth/me
Admin: /api/dashboard, /api/customers/**, /api/accounts/**, /api/loans/**
Customer: /api/customer/**

## 6. Customer credentials
When an admin creates a customer, the customer's email is used as login username and the supplied initial password becomes the first password. The customer can change it after login.

## 7. Banking rules
- Deposit/withdraw amount must be > 0.
- Withdraw cannot exceed available balance.
- Customer transactions are limited to the customer's own active accounts.
- Loan principal >= 10000.
- Interest > 0 and <= 50%.
- Tenure 1-480 months.
- Maximum 3 active loans.
- Active account balance must be >= 10% of principal.

## 8. Security teaching note
The included JWT secret fallback and demo credentials are for classroom use. Production systems must use secure secrets, stronger credential/bootstrap practices, HTTPS, appropriate token lifecycle controls, auditing and database migration tooling.

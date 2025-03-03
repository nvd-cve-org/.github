## **Submission & GitHub Repositories**
- **Backend**: [nvd-cve-backend](https://github.com/nvd-cve-org/nvd-cve-backend)
- **Frontend**: [nvd-cve-dashboard](https://github.com/nvd-cve-org/nvd-cve-dashboard)

# NVD CVE API Backend (`nvd-cve-backend`)

This project provides a backend API for managing and retrieving CVE (Common Vulnerabilities and Exposures) data. Built with **NestJS** and **TypeORM**, it offers endpoints for fetching CVE lists and retrieving details of specific CVEs.

## Features

✅ Retrieve a paginated list of CVEs  
✅ Fetch detailed information of a specific CVE by its ID  
✅ API Documentation using Swagger
✅ Support for filtering CVEs by year, severity score, and modification date  
✅ Sorting functionality (ascending/descending order)  
✅ Unit and E2E testing with Jest  
✅ CORS enabled for frontend integration  

## **Tech Stack**
- **Backend Framework**: NestJS  
- **Database ORM**: TypeORM  
- **Database**: PostgreSQL  
- **Testing**: Jest (Unit & E2E tests)  
- **Containerization**: Docker  
- **Environment Variables**: `.env` file  
- **Code Quality**: ESLint, Prettier
- **API Documentation**: Swagger

## **Setup Instructions**

### **1. Clone the repository**
```sh
git clone https://github.com/nvd-cve-org/nvd-cve-backend.git
cd nvd-cve-backend
```

### **2. Install dependencies**
```sh
yarn install
```

### **3. Set up environment variables**
Create a `.env` file in the root directory and configure it with:
```sh
DATABASE_URL=postgres://postgres:pLK0vU7lIZIQ2A4QqVIX@localhost:5432/nvd_cve_db
REDIS_HOST=localhost
REDIS_PORT=6379
```

### **4. Run database migrations**
```sh
yarn typeorm migration:run
```

### **5. Start the backend server**
```sh
yarn start
```

The server will run at **`http://localhost:8000`**.

### **6. Run tests**
#### **Unit Tests**
```sh
yarn test
```

#### **E2E Tests**
```sh
yarn test:e2e
```

# NVD CVE Dashboard Frontend (`nvd-cve-dashboard`)

This is a frontend dashboard built using **HTML**, **Javscript**, **Typescript**, **React**, **Next.js** and **TailwindCSS** to display a list of CVEs and their details.

## **Features**
✅ Paginated list of CVEs  
✅ Clickable rows to navigate to a detailed CVE page  
✅ Sorting options for CVEs (Published Date, Last Modified Date)  
✅ Adjustable page size (10, 50, 100 records per page)  
✅ Sorting order toggle (Ascending/Descending)  

## **Tech Stack**
- **Language**: Typescript
- **Frontend Framework**: Next.js  
- **UI Library**: TailwindCSS  
- **HTTP Client**: Axios  
- **State Management**: React Hooks  

## **Setup Instructions**

### **1. Clone the repository**
```sh
git clone https://github.com/nvd-cve-org/nvd-cve-dashboard.git
cd nvd-cve-dashboard
```

### **2. Install dependencies**
```sh
yarn install
```

### **3. Set up environment variables**
Create a `.env.local` file in the root directory and add:
```sh
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000
```

### **4. Start the frontend**
```sh
yarn dev
```
The app will be available at **`http://localhost:3000`**.

## **Screenshots**
<img width="1512" alt="image" src="https://github.com/user-attachments/assets/2d558b3c-6dd3-44f4-9aa3-2d37c7067453" />
<img width="1511" alt="image" src="https://github.com/user-attachments/assets/273770be-c6f2-4f9d-a05c-2381bf621f35" />

## **How the Frontend Communicates with Backend**
- Uses **Axios** for HTTP requests.
- Reads data from the **NestJS backend** via `NEXT_PUBLIC_API_BASE_URL`.
- Implements **client-side pagination** to enhance user experience.

---

# **Process & Implementation**
This section details how I approached and implemented each requirement of the assessment.

## 1. Consuming the CVE API & Storing Data
- Used NestJS with Axios to fetch data from the NVD API.
- Implemented pagination using startIndex and resultsPerPage to fetch all CVEs in chunks.
- Stored data in a PostgreSQL database using TypeORM.
- Normalized the data using multiple related tables such as:
  - cves: Stores core CVE information.
  - cve_descriptions: Stores multi-language descriptions.
  - cve_metrics: Stores severity scores (CVSS v2 & v3).
  - cve_configurations: Stores affected software configurations.
  - cve_weaknesses: Stores vulnerability classifications (CWE).
  - cve_references: Stores external reference links.
  
## 2. Data Cleansing & De-duplication
- Ensured data uniqueness by enforcing constraints on CVE ID as a primary key.
- Used `orIgnore` in TypeORM to handle duplicate entries efficiently.
- Validated API responses to remove null, empty, or malformed data before inserting.

## 3. Periodic Synchronization (Batch Mode)
- Implemented a cron job using node-cron to periodically fetch new CVEs.
The cron job runs every midnight.

## 4. API Endpoints to Read & Filter CVEs
Developed the following REST API endpoints using NestJS:

| Method | Endpoint | Description |
|--------|---------|-------------|
| GET	| /cves/list?page=1&limit=10 | Get paginated CVE list |
| GET	| /cves/:id | Get a specific CVE by ID |
| GET	| /cves/list?year=2023 | Get CVEs from a specific year |
| GET	| /cves/list?baseScore=9.8 | Filter CVEs by CVSS score |
| GET	| /cves/list?lastModifiedDays=30 | Get CVEs modified in the last N days |
| GET	| /cves/list?sortBy=publishedDate&sortOrder=ASC | Sort CVEs by date |

The API supports sorting, pagination, and filtering based on:

- CVE ID
- Year of publication
- CVSS base score
- Last modified date

## 5. Frontend UI to Visualize CVE Data
- Built a Next.js frontend with TypeScript and TailwindCSS.
- The homepage (/cves/list) displays a paginated table with:
- Total records count
- Adjustable results per page (10, 50, 100)
- Sorting options for Published Date and Last Modified Date
- Clickable CVE rows for detailed views
- The detail page (/cves/:id) fetches and displays full CVE details.

## 6. API Documentation
Documented API endpoints using Swagger (@nestjs/swagger).
Swagger UI available at:
```
http://localhost:8000/api
```

<img width="1506" alt="image" src="https://github.com/user-attachments/assets/5aad1a8f-ef60-4cc5-8bca-09694400cc9a" />
<img width="1426" alt="image" src="https://github.com/user-attachments/assets/e884b604-14cb-47d5-9741-8082dd636193" />
<img width="1420" alt="image" src="https://github.com/user-attachments/assets/2183b8a9-9808-4a6d-a63e-2c98fe5b57f8" />
<img width="1073" alt="image" src="https://github.com/user-attachments/assets/735f73f3-ff90-4b2c-98cc-fdd4206b9a1f" />


Clearly described:
- Query parameters for filtering CVEs
- Response structures
- Example requests and responses

## 7. Unit & E2E Testing
- Unit tests: Implemented using **Jest**, covering service logic and data retrieval.
- E2E tests: Used Supertest to verify API responses.
Covered:
- Fetching a single CVE
- Paginated API response
- Filtering & sorting behavior

Run tests using:
```
yarn test
```
For end-to-end tests:
```
yarn test:e2e
```

## 8. Code Quality & Best Practices
Used ESLint and Prettier for linting & formatting.
Implemented Docker support for easy deployment.

# Summary
- ✅ Fully functional CVE fetching and storage system
- ✅ Supports real-time synchronization & filtering
- ✅ User-friendly UI for CVE visualization
- ✅ Well-tested API with unit & E2E coverage
- ✅ Follows best practices for security & scalability

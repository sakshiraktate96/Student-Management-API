# Serverless Student Management API

## 1. Introduction

The Serverless Student Management API is a cloud-based REST API developed using AWS serverless services. The project provides functionality to manage student records through REST API operations.

The application uses Amazon API Gateway to receive client requests, AWS Lambda to process the requests, and Amazon DynamoDB to store student information.

The project implements complete CRUD operations:

* Create a student record
* Read student records
* Update a student record
* Delete a student record

---

## 2. Project Objective

The objective of this project is to build a serverless student management API using AWS services.

The project demonstrates:

* Serverless application development
* REST API implementation
* AWS Lambda function integration
* Amazon API Gateway configuration
* Amazon DynamoDB database operations
* IAM permissions
* API testing using AWS Management Console

---

## 3. AWS Services Used

### 3.1 Amazon API Gateway

Amazon API Gateway is used to create and expose the REST API endpoints.

It receives HTTP requests from the client and forwards them to the Lambda function.

### 3.2 AWS Lambda

AWS Lambda is used to execute the backend application code without managing servers.

The Lambda function processes the API requests and performs CRUD operations on DynamoDB.

### 3.3 Amazon DynamoDB

Amazon DynamoDB is used as the NoSQL database for storing student records.

The table used in the project was:

```text
Table Name: Students
Partition Key: studentId
Data Type: String
Billing Mode: On-Demand
```

### 3.4 AWS IAM

AWS IAM was used to provide the required permissions to the Lambda function.

An IAM execution role was created for the Lambda function to access DynamoDB.

---

## 4. Architecture

The project follows a serverless architecture:

```text
Client
   |
   v
Amazon API Gateway
   |
   v
AWS Lambda
   |
   v
Amazon DynamoDB
   |
   v
Student Records
```

### Architecture Flow

1. The client sends an HTTP request.
2. Amazon API Gateway receives the request.
3. API Gateway invokes the Lambda function.
4. Lambda processes the request.
5. Lambda performs the required operation on DynamoDB.
6. DynamoDB returns the result to Lambda.
7. Lambda sends the response back through API Gateway.
8. The client receives the API response.

---

## 5. DynamoDB Configuration

A DynamoDB table was created to store student information.

### Configuration

| Configuration | Value     |
| ------------- | --------- |
| Table Name    | Students  |
| Partition Key | studentId |
| Key Type      | String    |
| Billing Mode  | On-Demand |

### Student Record Structure

The student record contains the following attributes:

| Attribute | Description               |
| --------- | ------------------------- |
| studentId | Unique student identifier |
| name      | Student name              |
| email     | Student email address     |
| course    | Student course            |

### Sample Record

```json
{
  "studentId": "S102",
  "name": "Rahul Patil",
  "email": "rahul@example.com",
  "course": "MCA"
}
```

---

## 6. IAM Configuration

An IAM role was created for the Lambda function.

### IAM Role

```text
StudentLambdaDynamoDBRole
```

The role provided the Lambda function with the required DynamoDB permissions.

The role was attached to the Lambda function as its execution role.

---

## 7. Lambda Configuration

A Lambda function was created to implement the backend logic.

### Configuration

| Configuration  | Value                          |
| -------------- | ------------------------------ |
| Function Name  | StudentManagementAPI           |
| Runtime        | Python 3.14                    |
| Architecture   | x86_64                         |
| Handler        | lambda_function.lambda_handler |
| Execution Role | StudentLambdaDynamoDBRole      |

The Lambda function contains the logic for:

* Adding students
* Viewing all students
* Viewing a specific student
* Updating students
* Deleting students

---

## 8. API Gateway Configuration

A REST API was created using Amazon API Gateway.

### API Configuration

| Configuration | Value                |
| ------------- | -------------------- |
| API Name      | StudentManagementAPI |
| API Type      | REST API             |
| Endpoint Type | Regional             |
| Stage         | prod                 |

### API Resources

The following resources and methods were configured:

```text
/students
    ├── POST
    └── GET

/students/{studentId}
    ├── GET
    ├── PUT
    └── DELETE
```

Lambda Proxy Integration was used to connect API Gateway with the Lambda function.

---

## 9. API Operations

### 9.1 Add Student

**HTTP Method:**

```text
POST
```

**Endpoint:**

```text
/students
```

**Request Body:**

```json
{
  "studentId": "S102",
  "name": "Rahul Patil",
  "email": "rahul@example.com",
  "course": "MCA"
}
```

**Expected Result:**

```text
Status: 201
Student added successfully
```

The student record is stored in DynamoDB.

---

### 9.2 View All Students

**HTTP Method:**

```text
GET
```

**Endpoint:**

```text
/students
```

This operation retrieves all student records from the DynamoDB table.

**Result:**

```text
Status: 200
```

The API returns the available student records.

---

### 9.3 View One Student

**HTTP Method:**

```text
GET
```

**Endpoint:**

```text
/students/{studentId}
```

**Example:**

```text
/students/S102
```

**Result:**

```text
Status: 200
```

The API returns the details of the requested student.

---

### 9.4 Update Student

**HTTP Method:**

```text
PUT
```

**Endpoint:**

```text
/students/{studentId}
```

**Example:**

```text
/students/S102
```

**Request Body:**

```json
{
  "name": "Rahul Patil Updated",
  "email": "rahul.updated@example.com",
  "course": "MCA"
}
```

**Result:**

```text
Status: 200
Student updated successfully
```

The existing student information is updated in DynamoDB.

---

### 9.5 Delete Student

**HTTP Method:**

```text
DELETE
```

**Endpoint:**

```text
/students/{studentId}
```

**Example:**

```text
/students/S102
```

**Result:**

```text
Status: 200
Student deleted successfully
```

The specified student record is removed from DynamoDB.

---

## 10. Testing Results

All required CRUD operations were tested successfully through Amazon API Gateway.

| Operation         | Method | Status Code | Result     |
| ----------------- | ------ | ----------: | ---------- |
| Add Student       | POST   |         201 | Successful |
| View All Students | GET    |         200 | Successful |
| View One Student  | GET    |         200 | Successful |
| Update Student    | PUT    |         200 | Successful |
| Delete Student    | DELETE |         200 | Successful |

### Test Sequence

The testing was performed in the following order:

1. Added student `S102`.
2. Retrieved all students.
3. Retrieved student `S102`.
4. Updated student `S102`.
5. Deleted student `S102`.

All operations returned the expected responses.

---

## 11. Error Handling

The Lambda function includes exception handling to manage unexpected errors.

If a requested student does not exist, the API returns:

```text
Status: 404
Student not found
```

For invalid requests or unexpected errors, appropriate HTTP status codes and messages are returned.

---

## 12. Project Folder Structure

```text
Student-Management-API/
│
├── architecture/
│   └── architecture-diagram.png
│
├── documentation/
│   └── project-documentation.md
│
├── lambda/
│   └── lambda_function.py
│
├── screenshots/
│   ├── 05-POST-Add-Student-Test.png
│   ├── 06-DynamoDB-Student-Record.png
│   ├── 07-GET-View-All-Students.png
│   ├── 08-GET-View-One-Student.png
│   ├── 09-PUT-Update-Student.png
│   ├── 10-DELETE-Student.png
│   ├── 11-API-Gateway-POST-Test.png
│   ├── 12-API-Gateway-GET-All-Students.png
│   ├── 13-API-Gateway-GET-One-Student.png
│   ├── 14-API-Gateway-PUT-Update-Student.png
│   └── 15-API-Gateway-DELETE-Student.png
│
└── README.md
```

---

## 13. AWS Resource Cleanup

After completing the implementation and testing, the AWS resources created specifically for this project were deleted.

The following resources were cleaned up:

* Amazon API Gateway REST API
* AWS Lambda function
* DynamoDB `Students` table
* DynamoDB `students` table
* IAM execution role

The cleanup was performed after all required screenshots and testing results were captured.

---

## 14. Advantages of the Serverless Architecture

The serverless architecture provides several benefits:

* No server management is required.
* AWS Lambda executes code only when requests are received.
* DynamoDB provides a scalable NoSQL database.
* API Gateway provides managed REST API endpoints.
* The architecture can scale automatically according to demand.
* It is suitable for small applications and API-based workloads.

---

## 15. Conclusion

The Serverless Student Management API was successfully implemented using Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and AWS IAM.

The project successfully demonstrated the implementation of CRUD operations for student records.

All required API operations were tested successfully, including adding, viewing, updating, and deleting student records.

The project demonstrates the practical use of AWS serverless services to build a simple, scalable, and cost-efficient REST API without managing traditional servers.

# Serverless Student Management API

## Project Overview

The Serverless Student Management API is a cloud-based student management application built using AWS serverless services. The project provides REST APIs to add, view, update, and delete student records.

The application uses Amazon API Gateway to receive HTTP requests, AWS Lambda to process the requests, and Amazon DynamoDB to store student information.

## Objective

The main objective of this project is to build a serverless REST API for managing student records using AWS services.

The API supports the following operations:

* Add a student
* View all students
* View a specific student
* Update student information
* Delete a student

## AWS Services Used

| AWS Service        | Purpose                                             |
| ------------------ | --------------------------------------------------- |
| Amazon API Gateway | Creates and exposes REST API endpoints              |
| AWS Lambda         | Processes API requests and performs CRUD operations |
| Amazon DynamoDB    | Stores student records                              |
| AWS IAM            | Provides permissions for Lambda to access DynamoDB  |

## Architecture

The application follows this architecture:

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

### Request Flow

1. The client sends an HTTP request to Amazon API Gateway.
2. API Gateway forwards the request to the AWS Lambda function.
3. Lambda processes the request.
4. Lambda performs the required operation on the DynamoDB table.
5. The response is returned through API Gateway to the client.

## DynamoDB Configuration

### Table Name

```text
Students
```

### Partition Key

```text
studentId
```

### Key Type

```text
String
```

### Billing Mode

```text
On-Demand
```

## Lambda Configuration

### Function Name

```text
StudentManagementAPI
```

### Runtime

```text
Python 3.14
```

### Architecture

```text
x86_64
```

### Handler

```text
lambda_function.lambda_handler
```

The Lambda function performs all CRUD operations on the DynamoDB `Students` table.

## API Endpoints

Base API resource:

```text
/students
```

| Operation         | HTTP Method | Endpoint                | Purpose                      |
| ----------------- | ----------- | ----------------------- | ---------------------------- |
| Add Student       | POST        | `/students`             | Adds a new student           |
| View All Students | GET         | `/students`             | Retrieves all students       |
| View One Student  | GET         | `/students/{studentId}` | Retrieves a specific student |
| Update Student    | PUT         | `/students/{studentId}` | Updates student information  |
| Delete Student    | DELETE      | `/students/{studentId}` | Deletes a student            |

## Sample Student Data

```json
{
  "studentId": "S102",
  "name": "Rahul Patil",
  "email": "rahul@example.com",
  "course": "MCA"
}
```

## CRUD Testing

All required API operations were tested successfully through Amazon API Gateway.

### 1. Add Student

**Method:**

```text
POST /students
```

**Request:**

```json
{
  "studentId": "S102",
  "name": "Rahul Patil",
  "email": "rahul@example.com",
  "course": "MCA"
}
```

**Result:**

```text
Status: 201
Student added successfully
```

### 2. View All Students

**Method:**

```text
GET /students
```

**Result:**

```text
Status: 200
```

The API successfully returned the available student records.

### 3. View One Student

**Method:**

```text
GET /students/S102
```

**Result:**

```text
Status: 200
```

The API successfully returned the details of student `S102`.

### 4. Update Student

**Method:**

```text
PUT /students/S102
```

**Request:**

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

### 5. Delete Student

**Method:**

```text
DELETE /students/S102
```

**Result:**

```text
Status: 200
Student deleted successfully
```

## Testing Summary

| Test              | HTTP Method | Status | Result     |
| ----------------- | ----------- | -----: | ---------- |
| Add Student       | POST        |    201 | Successful |
| View All Students | GET         |    200 | Successful |
| View One Student  | GET         |    200 | Successful |
| Update Student    | PUT         |    200 | Successful |
| Delete Student    | DELETE      |    200 | Successful |

## Security and Permissions

AWS IAM was used to provide the required permissions to the Lambda function.

The Lambda execution role was configured with DynamoDB access permissions so that the function could perform database operations.

## Project Folder Structure

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

## Cleanup

After completing the testing and taking the required screenshots, the AWS resources created for this project were cleaned up.

The following resources were deleted:

* Amazon API Gateway REST API
* AWS Lambda function
* Amazon DynamoDB tables
* IAM execution role

This cleanup helps avoid unnecessary AWS resource usage after project completion.

## Conclusion

The Serverless Student Management API was successfully implemented using AWS Lambda, Amazon API Gateway, and Amazon DynamoDB.

All CRUD operations were tested successfully. The project demonstrates how AWS serverless services can be integrated to build a scalable and cost-efficient REST API for managing student records.
# Author 
Sakshi Raktate
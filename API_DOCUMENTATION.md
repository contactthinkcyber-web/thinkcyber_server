# ThinkCyber Dashboard API Documentation

## Base URL
```
http://localhost:3000/api
```

---

## 1. Dashboard Overview

### GET `/api/dashboard/overview`

Get comprehensive dashboard statistics including users, topics, enrollments, watch time, and growth metrics.

#### Request
```http
GET /api/dashboard/overview
```

#### Response (200 OK)
```json
{
  "success": true,
  "data": {
    "totalUsers": 16,
    "verifiedUsers": 12,
    "totalTopics": 31,
    "totalEnrollments": 45,
    "enrolledTopics": 45,
    "completedTopics": 28,
    "topicsInProgress": 17,
    "totalWatchTime": "125h 30m",
    "totalWatchTimeSeconds": 451800,
    "newUsersThisMonth": 2,
    "enrollmentsThisMonth": 8,
    "userGrowth": "+12.5%",
    "enrollmentGrowth": "+8.3%",
    "completionRate": "68.2%",
    "averageRating": "4.6"
  }
}
```

---

## 2. Dashboard Updates (User Enrollments)

### GET `/api/dashboard/updates`

Get paginated list of user enrollments and subscriptions with filtering options.

#### Query Parameters
| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| tab | string | No | Filter type: `enrolled` or `subscription` | `enrolled` |
| month | string | No | Filter by month (YYYY-MM format) | `2025-12` |
| fromDate | string | No | Start date (YYYY-MM-DD) | `2025-12-01` |
| toDate | string | No | End date (YYYY-MM-DD) | `2025-12-31` |
| page | integer | No | Page number (default: 1) | `1` |
| limit | integer | No | Items per page (default: 20) | `20` |

#### Request Examples
```http
GET /api/dashboard/updates?tab=enrolled&page=1&limit=20
GET /api/dashboard/updates?tab=subscription&month=2025-12
GET /api/dashboard/updates?fromDate=2025-12-01&toDate=2025-12-31
```

#### Response (200 OK)
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "userId": 5,
      "userName": "John Doe",
      "userEmail": "john@example.com",
      "topicId": 12,
      "topicTitle": "Introduction to Cybersecurity",
      "paymentStatus": "completed",
      "enrolledAt": "2025-12-01T10:30:00.000Z",
      "progress": 75,
      "watchTime": "2h 30m",
      "watchTimeSeconds": 9000,
      "subscriptionStartDate": "2025-12-01T10:30:00.000Z",
      "subscriptionEndDate": "2026-12-01T10:30:00.000Z",
      "subscriptionValidDays": 362,
      "isSubscriptionActive": true
    },
    {
      "id": 2,
      "userId": 8,
      "userName": "Jane Smith",
      "userEmail": "jane@example.com",
      "topicId": 15,
      "topicTitle": "Network Security Fundamentals",
      "paymentStatus": "active",
      "enrolledAt": "2025-12-03T14:20:00.000Z",
      "progress": 45,
      "watchTime": "1h 15m",
      "watchTimeSeconds": 4500,
      "subscriptionStartDate": null,
      "subscriptionEndDate": null,
      "subscriptionValidDays": 0,
      "isSubscriptionActive": false
    }
  ],
  "pagination": {
    "currentPage": 1,
    "totalPages": 3,
    "totalCount": 45,
    "limit": 20,
    "hasNextPage": true,
    "hasPrevPage": false
  },
  "filters": {
    "tab": "enrolled",
    "month": null,
    "fromDate": null,
    "toDate": null
  }
}
```

---

## 3. Monthly Earnings

### GET `/api/dashboard/earnings`

Get monthly revenue data based on successful payments.

#### Query Parameters
| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| year | integer | No | Target year (default: current year) | `2025` |
| months | integer | No | Number of months 1-12 (default: 12) | `12` |

#### Request Examples
```http
GET /api/dashboard/earnings
GET /api/dashboard/earnings?year=2025&months=12
GET /api/dashboard/earnings?year=2024&months=6
```

#### Response (200 OK)
```json
[
  { "month": "Jan", "value": 0 },
  { "month": "Feb", "value": 0 },
  { "month": "Mar", "value": 0 },
  { "month": "Apr", "value": 0 },
  { "month": "May", "value": 0 },
  { "month": "Jun", "value": 0 },
  { "month": "Jul", "value": 0 },
  { "month": "Aug", "value": 0 },
  { "month": "Sep", "value": 0 },
  { "month": "Oct", "value": 150 },
  { "month": "Nov", "value": 0 },
  { "month": "Dec", "value": 0 }
]
```

---

## 4. Monthly Growth Report

### GET `/api/dashboard/reports/monthly`

Get monthly growth report showing increased amounts in users, enrollments, and revenue.

#### Query Parameters
| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| year | integer | No | Target year (default: current year) | `2025` |
| months | integer | No | Number of months 1-12 (default: 12) | `12` |

#### Request Examples
```http
GET /api/dashboard/reports/monthly
GET /api/dashboard/reports/monthly?year=2025&months=12
GET /api/dashboard/reports/monthly?year=2024&months=6
```

#### Response (200 OK)
```json
{
  "success": true,
  "data": [
    {
      "month": "Jan",
      "users": 15,
      "enrollments": 45,
      "revenue": 150.00,
      "growth": "N/A"
    },
    {
      "month": "Feb",
      "users": 12,
      "enrollments": 38,
      "revenue": 0.00,
      "growth": "-15.6%"
    },
    {
      "month": "Mar",
      "users": 20,
      "enrollments": 60,
      "revenue": 0.00,
      "growth": "+57.9%"
    },
    {
      "month": "Apr",
      "users": 8,
      "enrollments": 25,
      "revenue": 0.00,
      "growth": "-58.3%"
    },
    {
      "month": "May",
      "users": 18,
      "enrollments": 55,
      "revenue": 0.00,
      "growth": "+120.0%"
    },
    {
      "month": "Jun",
      "users": 22,
      "enrollments": 70,
      "revenue": 0.00,
      "growth": "+27.3%"
    },
    {
      "month": "Jul",
      "users": 14,
      "enrollments": 42,
      "revenue": 0.00,
      "growth": "-40.0%"
    },
    {
      "month": "Aug",
      "users": 25,
      "enrollments": 80,
      "revenue": 0.00,
      "growth": "+90.5%"
    },
    {
      "month": "Sep",
      "users": 19,
      "enrollments": 58,
      "revenue": 0.00,
      "growth": "-27.5%"
    },
    {
      "month": "Oct",
      "users": 16,
      "enrollments": 48,
      "revenue": 150.00,
      "growth": "-17.2%"
    },
    {
      "month": "Nov",
      "users": 21,
      "enrollments": 65,
      "revenue": 0.00,
      "growth": "+35.4%"
    },
    {
      "month": "Dec",
      "users": 13,
      "enrollments": 40,
      "revenue": 0.00,
      "growth": "-38.5%"
    }
  ]
}
```

---

## 5. Monthly Report by Segment

### GET `/api/dashboard/reports/monthlyReport`

Generate detailed monthly reports for earnings, topics, or enrollments with optional CSV download.

#### Query Parameters
| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| segment | string | **Yes** | Report type: `earnings`, `topics`, or `enrolled` | `earnings` |
| month | string | No | Filter by month (YYYY-MM format) | `2025-12` |
| download | boolean | No | Download as CSV (default: false) | `true` |

### 5.1 Earnings Segment

Get payment transactions with revenue details.

#### Request
```http
GET /api/dashboard/reports/monthlyReport?segment=earnings&month=2025-12
```

#### Response (200 OK)
```json
{
  "success": true,
  "data": {
    "segment": "earnings",
    "month": "Dec 2025",
    "totalPaymentTransactions": 14,
    "totalTopics": 11,
    "totalEnrolled": 14,
    "totalSubscribed": 0,
    "data": [
      {
        "userId": 38,
        "userName": "Lakshmi Sujatha",
        "userEmail": "sujathanaidu@yahoo.com",
        "topicId": 314,
        "topicTitle": "Top Cyber Security issues in India",
        "amount": 0,
        "transactionStatus": "Pending",
        "paymentStatus": "pending",
        "date": "2025-12-04T12:03:12.814Z"
      },
      {
        "userId": 59,
        "userName": "Sai Charan",
        "userEmail": "anumasa52@gmail.com",
        "topicId": 310,
        "topicTitle": "Network Access and Authentication",
        "amount": 0,
        "transactionStatus": "Success",
        "paymentStatus": "completed",
        "date": "2025-12-01T13:41:10.709Z"
      },
      {
        "userId": 59,
        "userName": "Sai Charan",
        "userEmail": "anumasa52@gmail.com",
        "topicId": 72,
        "topicTitle": "Advanced Threat Intelligence & Analysis",
        "amount": 150,
        "transactionStatus": "Pending",
        "paymentStatus": "pending",
        "date": "2025-12-01T12:55:29.458Z"
      }
    ]
  }
}
```

#### Download CSV
```http
GET /api/dashboard/reports/monthlyReport?segment=earnings&month=2025-12&download=true
```

**CSV Format:**
```csv
User ID,User Name,User Email,Topic ID,Topic Title,Amount,Transaction Status,Payment Status,Date
5,"John Doe","john@example.com",12,"Introduction to Cybersecurity",0.00,Success,completed,2025-12-01T10:30:00.000Z
8,"Jane Smith","jane@example.com",15,"Network Security Fundamentals",0.00,Success,completed,2025-12-02T14:20:00.000Z
```

---

### 5.2 Topics Segment

Get all topics with enrollment statistics.

#### Request
```http
GET /api/dashboard/reports/monthlyReport?segment=topics&month=2025-12
```

#### Response (200 OK)
```json
{
  "success": true,
  "data": {
    "segment": "topics",
    "month": "Dec 2025",
    "totalPaymentTransactions": 4,
    "totalTopics": 31,
    "totalEnrolled": 4,
    "totalSubscribed": 0,
    "data": [
      {
        "topicId": 12,
        "topicTitle": "Introduction to Cybersecurity",
        "description": "Learn the fundamentals of cybersecurity",
        "price": 0.00,
        "totalEnrollments": 15,
        "completedEnrollments": 8,
        "averageProgress": "67.5"
      },
      {
        "topicId": 15,
        "topicTitle": "Network Security Fundamentals",
        "description": "Master network security concepts",
        "price": 0.00,
        "totalEnrollments": 12,
        "completedEnrollments": 5,
        "averageProgress": "54.2"
      },
      {
        "topicId": 18,
        "topicTitle": "Ethical Hacking Basics",
        "description": "Introduction to ethical hacking techniques",
        "price": 150.00,
        "totalEnrollments": 8,
        "completedEnrollments": 3,
        "averageProgress": "45.8"
      },
      {
        "topicId": 20,
        "topicTitle": "Advanced Penetration Testing",
        "description": "Advanced penetration testing methodologies",
        "price": 0.00,
        "totalEnrollments": 10,
        "completedEnrollments": 4,
        "averageProgress": "38.9"
      }
    ]
  }
}
```

#### Download CSV
```http
GET /api/dashboard/reports/monthlyReport?segment=topics&download=true
```

**CSV Format:**
```csv
Topic ID,Topic Title,Description,Price,Total Enrollments,Completed Enrollments,Average Progress
12,"Introduction to Cybersecurity","Learn the fundamentals of cybersecurity",0.00,15,8,67.5
15,"Network Security Fundamentals","Master network security concepts",0.00,12,5,54.2
```

---

### 5.3 Enrolled Segment

Get user enrollments with progress and watch time.

#### Request
```http
GET /api/dashboard/reports/monthlyReport?segment=enrolled&month=2025-12
#### Response (200 OK)
```json
{
  "success": true,
  "data": {
    "segment": "enrolled",
    "month": "Dec 2025",
    "totalPaymentTransactions": 4,
    "totalTopics": 3,
    "totalEnrolled": 4,
    "totalSubscribed": 0,
    "data": [
      {
        "userId": 5,
        "userName": "John Doe",
        "userEmail": "john@example.com",
        "topicId": 12,
        "topicTitle": "Introduction to Cybersecurity",
        "paymentStatus": "completed",
        "enrollmentStatus": "Active",
        "progress": "75.0",
        "watchTime": 9000,
        "enrolledAt": "2025-12-01T10:30:00.000Z"
      },
      {
        "userId": 8,
        "userName": "Jane Smith",
        "userEmail": "jane@example.com",
        "topicId": 15,
        "topicTitle": "Network Security Fundamentals",
        "paymentStatus": "completed",
        "enrollmentStatus": "Active",
        "progress": "45.0",
        "watchTime": 4500,
        "enrolledAt": "2025-12-02T14:20:00.000Z"
      },
      {
        "userId": 3,
        "userName": "Mike Johnson",
        "userEmail": "mike@example.com",
        "topicId": 18,
        "topicTitle": "Ethical Hacking Basics",
        "paymentStatus": "completed",
        "enrollmentStatus": "Active",
        "progress": "60.0",
        "watchTime": 7200,
        "enrolledAt": "2025-12-03T09:15:00.000Z"
      },
      {
        "userId": 11,
        "userName": "Sarah Williams",
        "userEmail": "sarah@example.com",
        "topicId": 20,
        "topicTitle": "Advanced Penetration Testing",
        "paymentStatus": "pending",
        "enrollmentStatus": "Pending",
        "progress": "0.0",
        "watchTime": 0,
        "enrolledAt": "2025-12-04T16:45:00.000Z"
      }
    ]
  }
}   }
  ]
}
```

#### Download CSV
```http
GET /api/dashboard/reports/monthlyReport?segment=enrolled&download=true
```

**CSV Format:**
```csv
User ID,User Name,User Email,Topic ID,Topic Title,Payment Status,Enrollment Status,Progress,Watch Time (seconds),Enrolled At
5,"John Doe","john@example.com",12,"Introduction to Cybersecurity",completed,Active,75.0,9000,2025-12-01T10:30:00.000Z
8,"Jane Smith","jane@example.com",15,"Network Security Fundamentals",completed,Active,45.0,4500,2025-12-02T14:20:00.000Z
```

---

## Error Responses

### 400 Bad Request
```json
{
  "success": false,
  "error": "Valid segment parameter required: earnings, topics, or enrolled"
}
```

### 404 Not Found
```json
{
  "success": false,
  "error": "Resource not found"
}
```

### 500 Internal Server Error
```json
{
  "success": false,
  "error": "Internal server error"
}
```

---

## Usage Examples

### Example 1: Get Dashboard Overview
```javascript
fetch('http://localhost:3000/api/dashboard/overview')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Example 2: Get Enrolled Users for December 2025
```javascript
fetch('http://localhost:3000/api/dashboard/updates?tab=enrolled&month=2025-12')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Example 3: Get Yearly Earnings
```javascript
fetch('http://localhost:3000/api/dashboard/earnings?year=2025&months=12')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Example 4: Download Earnings Report as CSV
```javascript
fetch('http://localhost:3000/api/dashboard/reports/monthlyReport?segment=earnings&month=2025-12&download=true')
  .then(response => response.blob())
  .then(blob => {
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'earnings_report_Dec_2025.csv';
    a.click();
  });
```

### Example 5: Get Monthly Growth Report
```javascript
fetch('http://localhost:3000/api/dashboard/reports/monthly?year=2025&months=12')
  .then(response => response.json())
  .then(data => console.log(data));
```

---

## Notes

1. **Payment Status Values:**
   - `completed` - Payment successfully completed
   - `paid` - Payment received
   - `pending` - Payment pending
   - `subscription` - Subscription payment
   - `active` - Active enrollment
   - `processing` - Payment processing

2. **Date Formats:**
   - Month filter: `YYYY-MM` (e.g., `2025-12`)
   - Date range: `YYYY-MM-DD` (e.g., `2025-12-01`)
   - Timestamps: ISO 8601 format

3. **Subscription Validity:**
   - Calculated as 1 year from enrollment date
   - Only applies to `completed` and `subscription` payment statuses
   - `subscriptionValidDays` shows remaining days
   - `isSubscriptionActive` indicates if currently active

4. **CSV Downloads:**
   - Set `download=true` to get CSV format
   - Response header: `Content-Type: text/csv`
   - Filename automatically generated based on segment and month

5. **Pagination:**
   - Default page size: 20 items
   - Maximum page size: 100 items
   - Use `page` and `limit` parameters to control

---

## Postman Collection

Import this collection to test all endpoints:

```json
{
  "info": {
    "name": "ThinkCyber Dashboard API",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Dashboard Overview",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/overview",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "overview"]
        }
      }
    },
    {
      "name": "Dashboard Updates - Enrolled",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/updates?tab=enrolled&month=2025-12&page=1&limit=20",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "updates"],
          "query": [
            {"key": "tab", "value": "enrolled"},
            {"key": "month", "value": "2025-12"},
            {"key": "page", "value": "1"},
            {"key": "limit", "value": "20"}
          ]
        }
      }
    },
    {
      "name": "Monthly Earnings",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/earnings?year=2025&months=12",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "earnings"],
          "query": [
            {"key": "year", "value": "2025"},
            {"key": "months", "value": "12"}
          ]
        }
      }
    },
    {
      "name": "Monthly Growth Report",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/reports/monthly?year=2025&months=12",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "reports", "monthly"],
          "query": [
            {"key": "year", "value": "2025"},
            {"key": "months", "value": "12"}
          ]
        }
      }
    },
    {
      "name": "Monthly Report - Earnings",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/reports/monthlyReport?segment=earnings&month=2025-12",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "reports", "monthlyReport"],
          "query": [
            {"key": "segment", "value": "earnings"},
            {"key": "month", "value": "2025-12"}
          ]
        }
      }
    },
    {
      "name": "Monthly Report - Topics",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/reports/monthlyReport?segment=topics&month=2025-12",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "reports", "monthlyReport"],
          "query": [
            {"key": "segment", "value": "topics"},
            {"key": "month", "value": "2025-12"}
          ]
        }
      }
    },
    {
      "name": "Monthly Report - Enrolled",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/reports/monthlyReport?segment=enrolled&month=2025-12",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "reports", "monthlyReport"],
          "query": [
            {"key": "segment", "value": "enrolled"},
            {"key": "month", "value": "2025-12"}
          ]
        }
      }
    },
    {
      "name": "Download Earnings CSV",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "http://localhost:3000/api/dashboard/reports/monthlyReport?segment=earnings&month=2025-12&download=true",
          "protocol": "http",
          "host": ["localhost"],
          "port": "3000",
          "path": ["api", "dashboard", "reports", "monthlyReport"],
          "query": [
            {"key": "segment", "value": "earnings"},
            {"key": "month", "value": "2025-12"},
            {"key": "download", "value": "true"}
          ]
        }
      }
    }
  ]
}
```

---

**Last Updated:** December 4, 2025  
**API Version:** 1.0.0

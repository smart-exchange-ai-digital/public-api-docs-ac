---
layout: page
title: "API Specification"
permalink: /api-specification/
nav_order: 2
---

# **Audience Connect Reporting Service API Specification**

## **Overview**

The Audience Connect Reporting Service provides REST APIs for retrieving partner reporting data for both supply and demand partners. The service offers flexible querying capabilities with support for multiple output formats and comprehensive filtering options.

**Base URL:** Login to Audience Connect console or reach out to your contact in Audience Connect

**API Version:** v1

**Content-Type:** `application/json` or `text/csv`

**Authentication:** API Key Authentication (Required)

## **Table of Contents**

1. [Supply Partner API](#supply-partner-api)
2. [Demand Partner API](#demand-partner-api)
3. [Error Handling](#error-handling)
4. [Authentication](#authentication)

## **Supply Partner API**

### **Get Supply Partner Statistics**

Retrieves supply partner reporting data with flexible filtering and output formatting.

**Endpoint:** `GET /api/v1/supply`

**Query Parameters**

| Parameters | Data Type | Required | Description | Example |
| :---- | :---- | :---- | :---- | :---- |
| `api_key` | String | Yes | API Key | `AbCdEfGhIjKlMnOpQrStUvWxYz1234567890` |
| `ssp_id` | String | Yes | Supply Partner ID in Audience Connect Platform | `123456` |
| `start_date` | String | Yes | Start Date (ISO 8601: YYYY-MM-DD) | `2026-01-01` |
| `end_date` | String | Yes | End Date (ISO 8601: YYYY-MM-DD) | `2026-01-31` |
| `dimensions` | String | Yes | Comma-separated dimensions | `date,hour,site_id,bundle_domain` |
| `metrics` | String | Yes | Comma-separated metrics | `ad_requests,impressions,revenue` |
| `output` | String | Yes | Output format (`json` or `csv`) | `json` |
| `site_id` | String | No | Filter by specific site ID(s) | `12345678` |
| `bundle_domain` | String | No | Filter by bundle IDs or domain names | `com.example.app,example.com` |
| `sort_by` | String | No | Sort results by dimension (allowed: date, hour, site_id) | `date` |
| `order` | String | No | Sort order (`asc` or `desc`) | `desc` |

#### **Available Dimensions**

1. `date` - Date in YYYY-MM-DD format
2. `hour` - Hour of the day (0-23)
3. `site_id` - Site identifier
4. `bundle_domain` - Bundle ID for apps or domain name for websites

#### **Available Metrics**

1. `ad_requests` - Total number of ad requests
2. `impressions` - Total number of impressions served
3. `revenue` - Total supply revenue

#### **Request Example**

```http
GET /api/v1/supply?api_key=AbCdEfGhIjKlMnOpQrStUvWxYz1234567890&ssp_id=123456&start_date=2026-01-01&end_date=2026-01-31&dimensions=date,hour,site_id,bundle_domain&metrics=ad_requests,impressions,revenue&output=json&site_id=12345678&bundle_domain=com.example.app,example.com&sort_by=date&order=desc
```

#### **Response Format (JSON)**

```json
[
  {
    "date": "2026-01-01",
    "hour": 10,
    "site_id": "site12345678",
    "bundle_domain": "com.example.app",
    "ad_requests": 1500,
    "impressions": 1200,
    "revenue": 45.67
  },
  {
    "date": "2026-01-01",
    "hour": 11,
    "site_id": "site12345678",
    "bundle_domain": "example.com",
    "ad_requests": 1800,
    "impressions": 1500,
    "revenue": 52.34
  }
]
```

#### **Response Format (CSV)**

When `output=csv`, the response will be a CSV file with headers:

```csv
date,hour,site_id,bundle_domain,ad_requests,impressions,revenue
2026-01-01,10,site12345678,com.example.app,1500,1200,45.67
2026-01-01,11,site12345678,example.com,1800,1500,52.34
```

## **Demand Partner API**

### **Get Demand Partner Statistics**

Retrieves demand partner reporting data with flexible filtering and output formatting.

**Endpoint:** `GET /api/v1/demand`

#### **Query Parameters**

| Parameters | Data Type | Required | Description | Example |
| :---- | :---- | :---- | :---- | :---- |
| `api_key` | String | Yes | API Key | `AbCdEfGhIjKlMnOpQrStUvWxYz1234567890` |
| `dsp_id` | String | Yes | Demand Partner ID in Audience Connect Platform | `123` |
| `start_date` | String | Yes | Start Date (ISO 8601: YYYY-MM-DD) | `2026-01-01` |
| `end_date` | String | Yes | End Date (ISO 8601: YYYY-MM-DD) | `2026-01-31` |
| `dimensions` | String | Yes | Comma-separated dimensions | `date,hour,endpoint_id,bundle_domain` |
| `metrics` | String | Yes | Comma-separated metrics | `bid_requests,impressions,revenue` |
| `output` | String | Yes | Output format (`json` or `csv`) | `json` |
| `endpoint_id` | String | No | Filter by specific endpoint ID | `456` |
| `bundle_domain` | String | No | Filter by bundle IDs or domain names | `com.example.app,example.com` |
| `sort_by` | String | No | Sort results by dimension (allowed: date, hour, endpoint_id) | `date` |
| `order` | String | No | Sort order (`asc` or `desc`) | `desc` |

#### **Available Dimensions**

1. `date` - Date in YYYY-MM-DD format
2. `hour` - Hour of the day (0-23)
3. `endpoint_id` - Endpoint identifier
4. `bundle_domain` - Bundle ID for apps or domain name for websites

#### **Available Metrics**

1. `bid_requests` - Total number of bid requests
2. `impressions` - Total number of impressions served
3. `revenue` - Total demand revenue

#### **Request Example**

```http
GET /api/v1/demand?api_key=AbCdEfGhIjKlMnOpQrStUvWxYz1234567890&dsp_id=123&start_date=2026-01-01&end_date=2026-01-31&dimensions=date,hour,endpoint_id,bundle_domain&metrics=bid_requests,impressions,revenue&output=json&endpoint_id=456&bundle_domain=com.example.app,example.com&sort_by=date&order=desc
```

#### **Response Format (JSON)**

```json
[
  {
    "date": "2026-01-01",
    "hour": 10,
    "endpoint_id": "endpoint456",
    "bundle_domain": "com.example.app",
    "bid_requests": 2000,
    "impressions": 1500,
    "revenue": 78.90
  },
  {
    "date": "2026-01-01",
    "hour": 11,
    "endpoint_id": "endpoint456",
    "bundle_domain": "example.com",
    "bid_requests": 2200,
    "impressions": 1800,
    "revenue": 89.12
  }
]
```

#### **Response Format (CSV)**

When `output=csv`, the response will be a CSV file with headers:

```csv
date,hour,endpoint_id,bundle_domain,bid_requests,impressions,revenue
2026-01-01,10,endpoint456,com.example.app,2000,1500,78.90
2026-01-01,11,endpoint456,example.com,2200,1800,89.12
```

## **Error Handling**

The API uses standard HTTP status codes and returns detailed error information in the response body.

### **Error Response Format**

```json
{
  "type": "about:blank",
  "title": "Error Title",
  "status": 400,
  "detail": "Detailed error message",
  "instance": "URI",
  "description": "Human-readable description of the error"
}
```

### **HTTP Status Codes**

| Status Code | Status | Description |
| :---- | :---- | :---- |
| `200` | Success | Request processed successfully |
| `400` | Bad Request | Invalid parameters, missing required fields, invalid date format |
| `401` | Unauthorized | Invalid API Key |
| `403` | Forbidden | Insufficient permissions to access the resource |
| `404` | Not Found | Endpoint not found or HTTP method not supported |
| `500` | Internal Server Error | Unexpected server error |

### **Common Error Scenarios**

#### **400 Bad Request \- Missing Required Parameters**

```json
{
  "type": "about:blank",
  "title": "Bad Request",
  "status": 400,
  "detail": "[start_date is required, output is required]",
  "instance": "/api/v1/supply",
  "description": "Required field(s) missing or contain(s) invalid field(s) value, please try again."
}
```

#### **400 Bad Request \- Invalid Date Format**

```json
{
  "type": "about:blank",
  "title": "Bad Request",
  "status": 400,
  "detail": "start_date must be in yyyy-MM-dd format",
  "instance": "/api/v1/demand",
  "description": "Required field(s) missing or contain(s) invalid field(s) value, please try again."
}
```

#### **400 Bad Request \- Invalid Output Format**

```json
{
  "type": "about:blank",
  "title": "Bad Request",
  "status": 400,
  "detail": "output must be either 'json' or 'csv'",
  "instance": "/api/v1/supply",
  "description": "Required field(s) missing or contain(s) invalid field(s) value, please try again."
}
```

#### **401 Unauthorized \- Invalid API Key**

```json
{
  "type": "about:blank",
  "title": "Unauthorized",
  "status": 401,
  "detail": "The API Key is invalid",
  "instance": "/api/v1/demand",
  "description": "The API Key is invalid, check configuration and try again."
}
```

#### **403 Forbidden \- Insufficient Permissions**

```json
{
  "type": "about:blank",
  "title": "Forbidden",
  "status": 403,
  "detail": "Access is denied",
  "instance": "/api/v1/supply",
  "description": "You are not authorized to access this resource."
}
```

## **Authentication**

The API uses API Key authentication for partner access. Each partner (Supply or Demand) has a unique API key that must be included in the request parameters.

### **Authentication Requirements**

1. API keys are **required** for all partner endpoints (`/api/v1/supply` and `/api/v1/demand`)
2. Supply Partner API keys can only access Supply Partner endpoints
3. Demand Partner API keys can only access Demand Partner endpoints
4. API keys are validated against the partner database
5. Invalid or missing API keys result in `401 Unauthorized` responses

### **Security Features**

1. API keys are stored securely in the database
2. Keys can be re-generated/deactivated if compromised
3. All API communications are encrypted in transit
4. Each partner can only access their own data
5. No cross-partner data access is permitted

---

<footer class="documentation-footer">
  <div class="footer-content">
    <p style="color: #ffffff !important; text-shadow: 2px 2px 4px rgba(0,0,0,0.8) !important; font-weight: bold !important; background-color: rgba(0,0,0,0.3) !important; padding: 8px 12px !important; border-radius: 6px !important; display: inline-block !important;">
      <strong style="color: #ffffff !important; text-shadow: 2px 2px 4px rgba(0,0,0,0.9) !important;">Questions or Issues?</strong> Please contact our API support team or <a href="https://github.com/smart-exchange-ai-digital/public-api-docs-ac/issues" target="_blank" style="color: #ffffff !important; text-decoration: underline !important; text-shadow: 2px 2px 4px rgba(0,0,0,0.8) !important;">create an issue on GitHub</a>.
    </p>
    <div class="footer-license">
      <hr>
      <p>&copy; 2026 AI Digital. All rights reserved.</p>
      <p>This documentation is proprietary and subject to the terms of your Partner Agreement. 
      <a href="https://github.com/smart-exchange-ai-digital/public-api-docs-ac/blob/main/LICENSE" target="_blank">View license terms</a> | 
      <a href="https://github.com/smart-exchange-ai-digital/public-api-docs-ac" target="_blank">GitHub Repository</a></p>
    </div>
  </div>
</footer>


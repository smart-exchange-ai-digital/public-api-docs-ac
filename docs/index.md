---
layout: home
title: "API Documentation"
permalink: /
---

# Welcome to Audience Connect API Documentation

This documentation provides comprehensive information about the Audience Connect Reporting Service API endpoints for both Supply and Demand partners.

## Quick Navigation

- **[Supply Partner API](api-specification#supply-partner-api)** - Retrieve supply partner reporting data
- **[Demand Partner API](api-specification#demand-partner-api)** - Access demand partner statistics  
- **[Authentication](api-specification#authentication)** - API key requirements and security
- **[Error Handling](api-specification#error-handling)** - Status codes and error responses

## API Overview

The Audience Connect Reporting Service provides REST APIs for retrieving partner reporting data with:

- ✅ **Flexible filtering** - Filter by date ranges, sites, and endpoints
- ✅ **Multiple output formats** - JSON and CSV support
- ✅ **Comprehensive metrics** - Revenue, impressions, requests, and more
- ✅ **Secure authentication** - API key-based access control
- ✅ **Partner isolation** - Supply and demand partners have separate access

## Getting Started

1. **Obtain your API key** from Audience Connect console or reach out to your contact in Audience Connect
2. **Choose your endpoint** - Supply (`/api/v1/supply`) or Demand (`/api/v1/demand`)
3. **Review the documentation** - Check parameters and response formats
4. **Make your first request** - Start with a basic date range query

## API Endpoints

| Endpoint | Purpose | Authentication |
|----------|---------|----------------|
| `GET /api/v1/supply` | Supply partner reporting data | Supply Partner API Key |
| `GET /api/v1/demand` | Demand partner reporting data | Demand Partner API Key |

---

<footer class="documentation-footer">
  <div class="footer-content">
    <p><strong>Need help?</strong> Contact our API support team for assistance with integration and troubleshooting.</p>
    <div class="footer-license">
      <hr>
      <p>&copy; 2026 AI Digital. All rights reserved.</p>
      <p>This documentation is proprietary and subject to the terms of your Partner Agreement. 
      See the <a href="https://github.com/smart-exchange-ai-digital/public-api-docs-ac/blob/main/LICENSE" target="_blank">license terms</a> and 
      <a href="https://github.com/smart-exchange-ai-digital/public-api-docs-ac" target="_blank">source repository</a> on GitHub.</p>
    </div>
  </div>
</footer>
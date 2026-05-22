# API Documentation

## Base URL
```
http://localhost:8000
```

## Endpoints

### Health Check
```
GET /health
```

Returns the health status of the API server.

**Response:**
```json
{
  "status": "ok"
}
```

**Status Code:** 200 OK

---

### Welcome
```
GET /
```

Returns a welcome message from the OctoFit Tracker API.

**Response:**
```json
{
  "message": "OctoFit Tracker API Server"
}
```

**Status Code:** 200 OK

---

## Error Handling

All errors return appropriate HTTP status codes with error messages in the response body.

### Common Error Responses

**400 Bad Request**
```json
{
  "error": "Invalid request parameters"
}
```

**404 Not Found**
```json
{
  "error": "Resource not found"
}
```

**500 Internal Server Error**
```json
{
  "error": "Internal server error"
}
```

---

## Authentication

Currently, the API does not require authentication. Future endpoints will include JWT-based authentication.

---

## Rate Limiting

Rate limiting will be implemented in a future release.

---

## Versioning

The API currently uses version 1 (v1). Future versions may be accessed via `/api/v1/` prefix.

---

## Testing

Test the API endpoints using:

### cURL
```bash
curl http://localhost:8000/health
curl http://localhost:8000/
```

### Postman
Import the Postman collection (docs/postman-collection.json) into Postman for easy testing.

### JavaScript/Fetch
```javascript
fetch('http://localhost:8000/health')
  .then(res => res.json())
  .then(data => console.log(data))
```

# Database Admin Panel

A web-based interface to test PostgreSQL database connections and explore the SuiteCRM schema.

## Files

- `index.html` - Main admin interface
- `db-admin.js` - Frontend JavaScript for database operations
- `rust_db_endpoints.rs` - Backend Rust endpoints (to be integrated)
- `README.md` - This documentation

## Setup

### 1. Configure Database Settings

Make sure your `config/settings.js` file has the correct Azure PostgreSQL credentials:

```javascript
DATABASE: {
    SERVER: 'model-earth-server.database.windows.net',
    DATABASE: 'ModelEarthDB',
    USERNAME: 'sqladmin',
    PASSWORD: 'your-actual-password',
    PORT: 5432,
    SSL: true
}
```

### 2. Start Backend Server

Add the database admin endpoints to your Rust backend:

1. Copy the code from `rust_db_endpoints.rs` into your main.rs or a separate module
2. Add the dependencies to Cargo.toml if not already present:
   ```toml
   [dependencies]
   actix-web = "4"
   sqlx = { version = "0.7", features = ["runtime-tokio-rustls", "postgres", "chrono", "uuid"] }
   serde = { version = "1.0", features = ["derive"] }
   serde_json = "1.0"
   chrono = { version = "0.4", features = ["serde"] }
   ```

3. Configure the routes in your main function:
   ```rust
   App::new()
       .app_data(web::Data::new(pool.clone()))
       .configure(configure_db_admin_routes)
       // ... other configurations
   ```

4. Start the server:
   ```bash
   cargo run -- serve
   ```

### 3. Access Admin Panel

1. Open `sql/admin/index.html` in your web browser
2. Or serve it via HTTP server:
   ```bash
   # From the project root
   python -m http.server 3000
   # Then visit: http://localhost:3000/sql/admin/
   ```

## Features

### Connection Testing
- Tests database connectivity
- Shows connection parameters (without exposing password)
- Displays server information and diagnostics
- Provides troubleshooting help

### Table Listing
- Lists first 10 database tables
- Shows estimated row counts
- Provides table descriptions
- Displays schema information

### Quick Actions
- Check specific tables (users, accounts)
- Execute simple SELECT queries
- Test database health status
- View connection diagnostics

### Logging
- Real-time operation logging
- Request/response tracking
- Error details and debugging info
- Clear log functionality

## API Endpoints

The admin panel expects these backend endpoints:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/db/test-connection` | GET | Test database connection |
| `/api/db/tables` | GET | List database tables |
| `/api/db/table/{name}` | GET | Get table information |
| `/api/db/query` | POST | Execute SELECT query |
| `/api/health` | GET | Health check |

## Response Format

All endpoints return JSON in this format:

```javascript
{
    "success": true,
    "message": "Operation completed",
    "error": null,
    "data": { /* actual data */ }
}
```

## Security Notes

⚠️ **Important Security Considerations:**

1. **Admin Access Only** - This panel should only be accessible to administrators
2. **Query Restrictions** - Only SELECT queries are allowed for safety
3. **Firewall Rules** - Ensure your Azure PostgreSQL allows connections from your IP
4. **SSL Encryption** - All connections use SSL/TLS encryption
5. **No Password Display** - Passwords are never shown in the interface

## Troubleshooting

### Common Issues

**Connection Refused**
- Check if Rust backend is running on port 8080
- Verify `cargo run -- serve` is active

**Database Connection Failed**
- Verify Azure PostgreSQL credentials in settings.js
- Check Azure firewall rules allow your IP address
- Confirm SSL settings are correct

**Tables Not Loading**
- Ensure database schema is properly initialized
- Check user permissions on PostgreSQL database
- Verify table names match expected SuiteCRM schema

**CORS Errors**
- Add CORS headers to your Rust backend
- Ensure frontend and backend domains match

### Debug Steps

1. **Check Browser Console** - Look for JavaScript errors
2. **Check Network Tab** - Verify API requests are being made
3. **Check Backend Logs** - Look for Rust server error messages
4. **Test Direct Connection** - Use `psql` to test database connectivity

### Example Manual Test

Test your Azure PostgreSQL connection manually:

```bash
psql "host=model-earth-server.database.windows.net port=5432 dbname=ModelEarthDB user=sqladmin password=your-password sslmode=require"
```

## Development

### Adding New Features

1. Add frontend functionality to `db-admin.js`
2. Add corresponding backend endpoint to `rust_db_endpoints.rs`
3. Update the HTML interface in `index.html`
4. Test thoroughly before deploying

### Testing Checklist

- [ ] Connection test works
- [ ] Tables list properly
- [ ] Individual table queries work
- [ ] Error handling displays correctly
- [ ] Logging captures all operations
- [ ] Security restrictions are enforced

## Production Deployment

For production use:

1. **Restrict Access** - Add authentication/authorization
2. **HTTPS Only** - Serve over secure connections
3. **Rate Limiting** - Prevent abuse of database queries
4. **Audit Logging** - Log all admin operations
5. **Backup Strategy** - Ensure database backups before any operations

Remember: This is a powerful tool that provides direct database access. Use responsibly!
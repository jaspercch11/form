# Incident Reporting System

A comprehensive incident reporting and management system with database integration.

## Features

- Incident reporting form
- File upload support
- Database storage
- User authentication
- Audit logging

## Local Development

1. Install dependencies:
```bash
npm install
```

2. Create a `.env` file based on `.env.example`:
```bash
cp .env.example .env
```

3. Update the `.env` file with your database credentials:
```
DATABASE_URL=postgresql://username:password@host:port/database?sslmode=require
LOGIN_DATABASE_URL=postgresql://username:password@host:port/database?sslmode=require
PORT=3000
UPLOAD_DIR=./uploads
```

4. Start the development server:
```bash
npm run dev
```

## Deployment

### Heroku

1. Create a new Heroku app
2. Add PostgreSQL addon
3. Set environment variables:
```bash
heroku config:set DATABASE_URL=your_database_url
heroku config:set LOGIN_DATABASE_URL=your_login_database_url
```

4. Deploy:
```bash
git push heroku main
```

### Railway

1. Connect your GitHub repository to Railway
2. Add environment variables in Railway dashboard
3. Deploy automatically

### Render

1. Create a new Web Service
2. Connect your GitHub repository
3. Set environment variables
4. Deploy

### Vercel

1. Import your GitHub repository
2. Set environment variables
3. Deploy

## Environment Variables

- `DATABASE_URL`: Main database connection string
- `LOGIN_DATABASE_URL`: Login database connection string
- `PORT`: Server port (default: 3000)
- `UPLOAD_DIR`: File upload directory

## Troubleshooting

### Form not submitting data to database

1. **Check environment variables**: Ensure `DATABASE_URL` is set correctly
2. **Check database connection**: Verify your database is accessible
3. **Check server logs**: Look for error messages in the console
4. **Check CORS**: Ensure CORS is properly configured for your domain

### Common Issues

1. **Database connection failed**: 
   - Verify database URL format
   - Check if database is accessible from your hosting provider
   - Ensure SSL settings are correct

2. **Port issues**:
   - Most hosting providers set their own PORT environment variable
   - The app will automatically use `process.env.PORT || 3000`

3. **File upload issues**:
   - Ensure upload directory exists and is writable
   - Check file size limits

## Database Schema

The application expects the following tables:
- `incidents`: For storing incident reports
- `users`: For user authentication
- `activities`: For audit logging
- `policy_documents`: For document management
- `regulations`: For regulatory compliance
- `risks`: For risk management
- `heatmap_risks`: For risk heatmap

## API Endpoints

- `POST /submit-incident`: Submit a new incident
- `POST /login`: User authentication
- `GET /api/incidents`: Get all incidents
- `PUT /api/incidents/:id/status`: Update incident status
- `POST /api/documents/upload`: Upload documents
- `GET /api/dashboard/compliance-status`: Get compliance status
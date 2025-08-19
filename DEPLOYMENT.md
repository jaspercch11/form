# Deployment Guide

This guide will help you deploy your incident reporting system to various hosting platforms.

## Prerequisites

1. Your code is pushed to GitHub
2. You have your database connection strings ready
3. You have an account on your chosen hosting platform

## Platform-Specific Deployment

### 1. Railway

Railway is one of the easiest platforms for Node.js deployment.

1. **Sign up** at [railway.app](https://railway.app)
2. **Connect GitHub**: Click "New Project" → "Deploy from GitHub repo"
3. **Select your repository**
4. **Add Environment Variables**:
   - Go to your project → Variables tab
   - Add the following variables:
     ```
     DATABASE_URL=your_main_database_url
     LOGIN_DATABASE_URL=your_login_database_url
     PORT=3000
     ```
5. **Deploy**: Railway will automatically deploy when you push to GitHub

### 2. Render

Render offers free hosting with automatic deployments.

1. **Sign up** at [render.com](https://render.com)
2. **Create Web Service**:
   - Connect your GitHub repository
   - Choose "Web Service"
   - Set build command: `npm install`
   - Set start command: `npm start`
3. **Add Environment Variables**:
   - Go to Environment tab
   - Add your database URLs
4. **Deploy**: Render will deploy automatically

### 3. Heroku

Heroku is a popular platform with good Node.js support.

1. **Install Heroku CLI**:
   ```bash
   npm install -g heroku
   ```

2. **Login to Heroku**:
   ```bash
   heroku login
   ```

3. **Create Heroku app**:
   ```bash
   heroku create your-app-name
   ```

4. **Add PostgreSQL** (optional):
   ```bash
   heroku addons:create heroku-postgresql:mini
   ```

5. **Set environment variables**:
   ```bash
   heroku config:set DATABASE_URL=your_database_url
   heroku config:set LOGIN_DATABASE_URL=your_login_database_url
   ```

6. **Deploy**:
   ```bash
   git push heroku main
   ```

### 4. Vercel

Vercel is great for frontend-heavy applications.

1. **Sign up** at [vercel.com](https://vercel.com)
2. **Import project** from GitHub
3. **Configure**:
   - Framework preset: Node.js
   - Build command: `npm install`
   - Output directory: `.`
4. **Add Environment Variables** in the dashboard
5. **Deploy**

## Environment Variables Setup

For all platforms, you need to set these environment variables:

```
DATABASE_URL=postgresql://username:password@host:port/database?sslmode=require
LOGIN_DATABASE_URL=postgresql://username:password@host:port/database?sslmode=require
PORT=3000
```

## Database Setup

### Using Neon (Recommended)

1. **Sign up** at [neon.tech](https://neon.tech)
2. **Create a new project**
3. **Get your connection string** from the dashboard
4. **Set it as your DATABASE_URL**

### Using Supabase

1. **Sign up** at [supabase.com](https://supabase.com)
2. **Create a new project**
3. **Get your connection string** from Settings → Database
4. **Set it as your DATABASE_URL**

## Troubleshooting Deployment Issues

### 1. Form Not Submitting Data

**Symptoms**: Form submits but no data appears in database

**Solutions**:
- Check environment variables are set correctly
- Verify database connection string format
- Check server logs for errors
- Test database connection using the `/health` endpoint

### 2. Database Connection Failed

**Symptoms**: Server starts but can't connect to database

**Solutions**:
- Verify database URL format
- Check if database allows external connections
- Ensure SSL settings are correct
- Test connection locally first

### 3. Port Issues

**Symptoms**: App won't start or shows port already in use

**Solutions**:
- Most platforms set their own PORT environment variable
- The app automatically uses `process.env.PORT || 3000`
- Don't hardcode port numbers

### 4. File Upload Issues

**Symptoms**: Files not uploading or server errors

**Solutions**:
- Ensure upload directory exists
- Check file size limits
- Verify file permissions
- Consider using cloud storage for production

## Testing Your Deployment

1. **Health Check**: Visit `https://your-app-url/health`
2. **Form Submission**: Try submitting a test incident
3. **Database Verification**: Check if data appears in your database
4. **Error Logs**: Monitor server logs for any errors

## Security Considerations

1. **Environment Variables**: Never commit `.env` files to Git
2. **Database Security**: Use strong passwords and SSL connections
3. **CORS**: Configure CORS properly for your domain
4. **File Uploads**: Validate file types and sizes
5. **Input Validation**: Sanitize all user inputs

## Monitoring and Maintenance

1. **Logs**: Regularly check application logs
2. **Database**: Monitor database performance and connections
3. **Updates**: Keep dependencies updated
4. **Backups**: Regular database backups
5. **Health Checks**: Use the `/health` endpoint for monitoring
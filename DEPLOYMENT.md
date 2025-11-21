# Deployment Guide

This guide explains how to deploy the Hello World Express.js server to AWS Lambda or EC2.

## Local Development

To run the server locally:

```bash
npm install
npm start
```

The server will start on port 3000 (or the PORT environment variable if set).

### Available Endpoints

- `GET /` - Returns a Hello World message with timestamp
- `GET /health` - Health check endpoint

## AWS Lambda Deployment

### Prerequisites

- AWS CLI configured with appropriate credentials
- AWS Lambda function created

### Build for Lambda

```bash
npm run build:lambda
```

This creates a `lambda-deployment.zip` file containing all necessary files.

### Deploy to Lambda

1. Build the deployment package:
   ```bash
   npm run build:lambda
   ```

2. Upload to AWS Lambda:
   ```bash
   aws lambda update-function-code \
     --function-name your-function-name \
     --zip-file fileb://lambda-deployment.zip
   ```

3. Configure the handler:
   - Handler: `lambda.handler`
   - Runtime: Node.js 18.x or later

### Lambda Configuration

- **Handler**: `lambda.handler`
- **Runtime**: Node.js 18.x or later
- **Memory**: 128 MB (minimum)
- **Timeout**: 30 seconds

## AWS EC2 Deployment

### Prerequisites

- EC2 instance with Node.js installed
- SSH access to the instance

### Deploy to EC2

1. Clone the repository on your EC2 instance:
   ```bash
   git clone <repository-url>
   cd aos-cicd-demo
   ```

2. Install dependencies:
   ```bash
   npm run build:ec2
   ```

3. Start the server:
   ```bash
   npm start
   ```

4. (Optional) Use PM2 for process management:
   ```bash
   npm install -g pm2
   pm2 start index.js --name "hello-world-api"
   pm2 save
   pm2 startup
   ```

### Environment Variables

- `PORT` - Server port (default: 3000)
- `NODE_ENV` - Environment name (development/production)

### Security Considerations

1. Configure security groups to allow HTTP traffic on your chosen port
2. Consider using a reverse proxy (nginx) for production
3. Set up SSL/TLS certificates for HTTPS
4. Use environment variables for sensitive configuration

## Testing the Deployment

After deployment, test the endpoints:

```bash
# Test main endpoint
curl https://your-domain.com/

# Test health check
curl https://your-domain.com/health
```

Expected response from main endpoint:
```json
{
  "message": "Hello World!",
  "timestamp": "2024-01-01T00:00:00.000Z",
  "environment": "production"
}
```

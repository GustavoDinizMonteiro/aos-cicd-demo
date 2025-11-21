# aos-cicd-demo

Simple Hello World Express.js server with AWS Lambda and EC2 deployment support.

## Quick Start

```bash
# Install dependencies
npm install

# Run locally
npm start
```

Visit `http://localhost:3000` to see the Hello World message.

## Features

- ✅ Express.js web server
- ✅ Hello World endpoint (`/`)
- ✅ Health check endpoint (`/health`)
- ✅ AWS Lambda deployment support
- ✅ AWS EC2 deployment support
- ✅ Production-ready build scripts

## Endpoints

- `GET /` - Returns Hello World message with timestamp
- `GET /health` - Health check endpoint

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed deployment instructions for AWS Lambda and EC2.

## Scripts

- `npm start` - Start the server locally
- `npm run dev` - Run in development mode
- `npm run build:lambda` - Build deployment package for AWS Lambda
- `npm run build:ec2` - Prepare for EC2 deployment
- `npm test` - Simple smoke test

## Requirements

- Node.js 18.x or later
- npm 8.x or later
# Create URL Shortener API

## Overview

This project implements a serverless API for creating short URLs using AWS Lambda and S3. It allows generating unique codes for original URLs and storing them with an expiration time.

## Features

- Generation of unique short codes for long URLs
- Support for configuring expiration time
- Storage of data in S3 bucket
- Response with the generated short URL code

## Architecture

The application consists of:

1. **AWS Lambda Function**: Processes HTTP requests to create short URLs
2. **Amazon S3**: Stores the mapping data between short URLs and original ones
3. **Data Model**: Representation of URL data with expiration time

## How It Works

1. The client sends a POST request containing the original URL and expiration time
2. The Lambda function generates a unique 8-character code (based on UUID)
3. The function creates a JSON object with the original URL and expiration time
4. The object is stored in the S3 bucket with the name `{code}.json`
5. The API returns the generated code to the client

## File Structure

- `Main.java`: Main class that implements the Lambda function handler
- `UrlData.java`: Model class for URL data

## Request Format

```json
{
    "originalUrl": "https://example.com/page-with-very-long-url",
    "expirationTime": "1640995200"
}
```

Where `expirationTime` is the Unix timestamp (in seconds) that defines when the URL expires.

## Response Format

```json
{
    "code": "a1b2c3d4"
}
```

This code should be used to compose the final short URL, for example: `https://yourdomain.com/a1b2c3d4`

## Technologies Used

- Java
- AWS Lambda
- Amazon S3
- Jackson (for JSON processing)
- Lombok (for boilerplate reduction)
- AWS SDK for Java v2

## Requirements

- JDK 11 or higher
- Maven
- AWS CLI configured with appropriate credentials
- S3 bucket configured for data storage

## Configuration

To use this application, you need to:

1. Create an S3 bucket named `url-shortener-devjf` (or change the name in the code)
2. Configure Lambda to be triggered by HTTP requests via API Gateway
3. Set up the necessary permissions for Lambda to access the S3 bucket
4. Configure API Gateway to accept POST requests with JSON body

## Integration

This service works in conjunction with the short URL redirection API. After creating a short URL with this API, the returned code can be used with the redirection service to access the original URL.

## Security Considerations

- The code generation uses UUID to minimize collisions
- No URL validation is performed - consider implementing validation to prevent malicious redirects
- No authentication/authorization is implemented in this basic example

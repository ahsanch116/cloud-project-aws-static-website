# AWS Static Website Hosting with S3

This project demonstrates how to host a static website using Amazon S3. The website will be accessible via the default S3 endpoint without the need for a custom domain. The guide includes instructions for setting up the S3 buckets, configuring the website, and handling error pages like 404.

## Project Overview

- **Bucket 1:** `example-bucket` (for hosting the website content)
- **Bucket 2:** `example-bucket-logs` (for storing access logs)

## Prerequisites

- An AWS account
- Basic knowledge of S3 and AWS services
- Here is how your architecture will look like:
![Network Diagrams (1)](https://github.com/user-attachments/assets/67555f80-4c03-4514-a6a4-3d18e4858071)

## Steps to Create the Project

### 1. Create S3 Buckets

- **Bucket 1 (Website Content):** 
  - Name: `example-bucket`
  - Region: `eu-north-1` (or your preferred region)
  - Enable static website hosting
  - Set the index document to `index.html`
  - Set the error document to `error.html` or `404.html`

- **Bucket 2 (Access Logs):**
  - Name: `example-bucket-logs`
  - Region: Same as the first bucket
  - Enable logging and configure the destination to `example-bucket-logs`

### 2. Upload Website Content

1. **index.html** - This is your main webpage file. Here’s a simple example:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Welcome to My Website</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                text-align: center;
                margin-top: 50px;
            }
        </style>
    </head>
    <body>
        <h1>Welcome to My AWS Hosted Website!</h1>
        <p>This is a static website hosted on Amazon S3.</p>
    </body>
    </html>
    ```

2. **404.html (or error.html)** - This file will be displayed if a user tries to access a page that doesn't exist. Here’s a basic example:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>404 - Page Not Found</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                text-align: center;
                margin-top: 50px;
            }
            h1 {
                color: red;
            }
        </style>
    </head>
    <body>
        <h1>404 - Page Not Found</h1>
        <p>Oops! The page you are looking for does not exist.</p>
    </body>
    </html>
    ```

### 3. Configure Bucket Policies (Optional)

You may need to configure bucket policies to allow public access to the website. Here’s an example policy:
  ```json
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Principal": "*",
              "Action": "s3:GetObject",
              "Resource": "arn:aws:s3:::example-bucket/*"
           }
        ]
  }
```

## 4. Enable Logging

Configure logging for your website bucket and direct logs to `example-bucket-logs`.

## 5. Test Your Website

### Access Your Website:
- Go to the S3 bucket's website endpoint. It will look something like `http://example-bucket.s3-website.eu-north-1.amazonaws.com`.
- Your `index.html` page should be displayed.
- Example:![website pic](https://github.com/user-attachments/assets/cc8243e2-9dba-436e-8426-fef4849ed776)


### Test Error Handling:
- Try accessing a non-existent page like `http://example-bucket.s3-website.eu-north-1.amazonaws.com/nonexistentpage.html`.
- The 404 error page should appear.

## Optional Enhancements

If you want to further improve the performance and security of your website, consider integrating CloudFront for content delivery and enabling HTTPS.

## Conclusion

This project is a simple example of how to host a static website on AWS using S3. By following the steps outlined in this guide, you can create and deploy a basic website accessible to the public.

Feel free to modify the HTML files and bucket configurations to suit your specific needs.

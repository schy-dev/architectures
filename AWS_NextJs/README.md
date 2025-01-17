# AWS Architecture for Next.js Deployment

## Solution Overview

This solution deploys a Next.js application behind an Nginx proxy on AWS, ensuring seamless routing between a new Next.js app and an existing live website. Here's how it works:

### Components

1. **Route 53**
   - Handles DNS and directs all incoming traffic to AWS resources.

2. **CloudFront**
   - Acts as a Content Delivery Network (CDN) to cache content, improve performance, and reduce latency.
   - Provides HTTPS support for secure communication.

3. **Application Load Balancer (ALB)**
   - Central routing component.
   - Routes traffic to different destinations based on URL paths:
     - `/jobs` requests are sent to the new Next.js application.
     - All other requests are sent to the existing website hosted on S3.

4. **ECS (Elastic Container Service)**
   - Hosts the new Next.js application in a containerized environment.
   - Provides scalability and efficient resource usage.

5. **S3 Bucket**
   - Hosts the existing static website.
   - Serves all requests except for `/jobs`.

### How It Works

1. **DNS Resolution:**
   - Route 53 resolves the domain and forwards all traffic to CloudFront.

2. **Content Caching:**
   - CloudFront reduces latency and offloads traffic with caching capabilities.

3. **Traffic Routing:**
   - The ALB examines the request path:
     - If the path is `/jobs`, it forwards the request to the ECS service running the Next.js app.
     - For other paths, it directs the request to the S3 bucket hosting the existing website.

4. **Scalability and Security:**
   - ECS scales dynamically to handle traffic spikes for the Next.js app.
   - SSL certificates from ACM ensure secure HTTPS communication.

### Benefits
- Simplified routing and management.
- High scalability and performance.
- Secure and reliable architecture.
- Clear separation of responsibilities between the new application and the existing website.

This architecture ensures seamless integration of a new Next.js application with minimal disruption to the existing setup, while leveraging AWS services for scalability and reliability.

Link to the diagram
https://app.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1#Hschy-dev/architectures/main/Untitled%20Diagram.drawio#%7B%22pageId%22%3A%22C5RBs43oDa-KdzZeNtuy%22%7D 

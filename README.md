# *Product Management System with Asynchronous Image Processing*

## *Overview*
This project is a backend system for a product management application built using Go. The system is designed for high performance, scalability, and modularity, incorporating advanced features such as asynchronous image processing, caching, structured logging, and robust error handling.

---

## *Key Features*
*Product Management API*:   - Add products with details such as name, description, price, and image URLs.
   - Retrieve product details by ID, including processed image data.
   - List all products for a user with optional filters for price and name.

*Asynchronous Image Processing*:   - Processes product images in the background without blocking API responses.
   - Compresses images and uploads them to cloud storage (e.g., S3).
   - Updates the database with URLs of compressed images.

*Caching with Redis*:   - Caches product data to improve API response times.
   - Implements cache invalidation to reflect real-time updates.

*Scalability*:   - Modular architecture allows independent scaling of API and worker services.
   - Designed to handle high API traffic and large data volumes.

*Structured Logging*:   - Logs all events, including API requests, image processing steps, and errors, using tools like logrus or zap.

*Robust Error Handling*:   - Ensures transactional consistency across the database, cache, and message queue.
   - Uses retries and dead-letter queues for failed tasks.

*Comprehensive Testing*:   - Unit tests for core functions.
   - Integration tests for seamless workflow validation.
   - Benchmarking for key endpoints like GET /products/:id.

---

## *System Architecture*
The system is designed with a *modular architecture*:
*API Service*: Handles user requests and interacts with the database and cache.
*Worker Service*: Processes images asynchronously.
*Redis Cache*: Stores frequently accessed product data.
*PostgreSQL Database*: Stores product and user information.
*Message Queue*: RabbitMQ or Kafka for managing asynchronous image processing tasks.
---

## *Endpoints*

### *1. POST /products*
*Description*: Adds a new product to the database and queues image URLs for processing.  
*Request Body*:
json
{
  "user_id": 1,
  "product_name": "Smartphone",
  "product_description": "Latest model with advanced features",
  "product_images": ["https://example.com/image1.jpg", "https://example.com/image2.jpg"],
  "product_price": 999.99
}

*Response*:
json
{
  "message": "Product created successfully",
  "product_id": 101
}


---

### *2. GET /products/:id*
*Description*: Retrieves product details by ID, including processed images.  
*Response*:
json
{
  "id": 101,
  "user_id": 1,
  "product_name": "Smartphone",
  "product_description": "Latest model with advanced features",
  "product_images": ["https://example.com/image1.jpg", "https://example.com/image2.jpg"],
  "compressed_product_images": ["https://s3.amazonaws.com/image1_compressed.jpg"],
  "product_price": 999.99
}


---

### *3. GET /products*
*Description*: Retrieves all products for a user with optional filters for price and name.  
*Query Parameters*:
user_id (required)
price_min (optional)
price_max (optional)
product_name (optional)  
*Response*:
json
[
  {
    "id": 101,
    "user_id": 1,
    "product_name": "Smartphone",
    "product_description": "Latest model with advanced features",
    "product_price": 999.99
  }
]


---

## *Installation and Setup*

### *1. Prerequisites*
Install Go (version 1.19+).
Set up PostgreSQL and create the required database schema.
Install Redis.
Install RabbitMQ or Kafka for the message queue.
### *2. Clone the Repository*
bash
git clone https://github.com/your-username/product-management.git
cd product-management


### *3. Configure Environment Variables*
Create a .env file with the following:

DB_HOST=localhost
DB_PORT=5432
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_NAME=product_db
REDIS_HOST=localhost
REDIS_PORT=6379
QUEUE_HOST=localhost
QUEUE_PORT=5672
AWS_S3_BUCKET=your_s3_bucket_name
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret


### *4. Run Database Migrations*
bash
go run cmd/migrate/main.go


### *5. Start the API Server*
bash
go run cmd/api/main.go


### *6. Start the Worker Service*
bash
go run cmd/worker/main.go


---

## *Testing*
Run tests using the following command:
bash
go test ./...


---

## *Future Enhancements*
Add authentication and authorization for API endpoints.
Implement support for bulk product uploads.
Extend caching to additional endpoints.
---

## *Why This Project?*
This project demonstrates advanced backend development skills, including:
Building scalable systems using *Go*.
Working with databases, caching, and message queues.
Handling real-world challenges like asynchronous processing and transactional consistency.
It highlights my ability to design and implement solutions that are robust, efficient, and aligned with modern backend development best practices.

---





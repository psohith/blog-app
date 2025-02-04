# Blog API Documentation

## Overview
This is a Django REST Framework-based blog application that allows users to create, edit, delete, and view blogs. Users can also comment on blogs and view previous versions of edited blogs. The API uses JWT authentication for security.

## API Endpoints

### Authentication
#### Register
**Endpoint:** `POST /register/`
- Registers a new user.
- **Request Body:**
  ```json
  {
    "username": "testuser",
    "email": "test@example.com",
    "password": "password123"
  }
  ```
- **Response:**
  ```json
  {
    "username": "testuser",
    "email": "test@example.com"
  }
  ```

#### Login
**Endpoint:** `POST /login/`
- Authenticates a user and returns JWT tokens.
- **Request Body:**
  ```json
  {
    "username": "testuser",
    "password": "password123"
  }
  ```
- **Response:**
  ```json
  {
    "refresh": "token_here",
    "access": "token_here"
  }
  ```

### Blog Management
#### Create a Blog
**Endpoint:** `POST /blog/`
- Creates a new blog post.
- **Authentication Required**
- **Request Body:**
  ```json
  {
    "title": "My First Blog",
    "content": "This is my blog content"
  }
  ```
- **Response:**
  ```json
  {
    "id": "1",
    "title": "My First Blog",
    "content": "This is my blog content",
    "author": 1
  }
  ```

#### View User Blogs
**Endpoint:** `GET /blog/`
- Retrieves blogs created by the authenticated user.
- Supports search functionality via query parameter `?search=<keyword>`

#### View a Specific Blog
**Endpoint:** `GET /blog/<blog_id>/`
- Retrieves details of a specific blog.
- **Authentication Required**

#### Edit a Blog
**Endpoint:** `PATCH /blog/<blog_id>/`
- Partially updates a blog post.
- **Authentication Required**
- **Request Body:**
  ```json
  {
    "title": "Updated Blog Title"
  }
  ```

#### Delete a Blog
**Endpoint:** `DELETE /blog/<blog_id>/`
- Deletes a blog post.
- **Authentication Required**

#### View Blog Versions
**Endpoint:** `GET /blogVersions/<blog_id>/`
- Retrieves previous versions of a blog post.
- **Authentication Required**

### Comment Management
#### Add a Comment
**Endpoint:** `POST /comment/`
- Adds a comment to a blog post.
- **Authentication Required**
- **Request Body:**
  ```json
  {
    "blog": "1",
    "content": "Great post!"
  }
  ```

### Public Blog Access
#### View All Blogs
**Endpoint:** `GET /all`
- Retrieves all public blogs.
- Supports search functionality via query parameter `?search=<keyword>`

## Authentication
- The API uses JWT authentication.
- Clients must include the `Authorization: Bearer <access_token>` header in requests that require authentication.

## Pagination
- Blogs and comments are paginated, with a default limit of 5 items per page.
- To request a specific page, use the `?page=<number>` query parameter.

## Models
### Blog
- `id`: Unique identifier
- `title`: Blog title
- `content`: Blog content
- `author`: User who created the blog
- `created_at`: Timestamp of creation
- `updated_at`: Timestamp of last update

### BlogVersion
- Stores previous versions of edited blogs.

### Comment
- `id`: Unique identifier
- `content`: Comment text
- `blog`: Associated blog post
- `author`: User who posted the comment

## Security Considerations
- Only authenticated users can create, edit, or delete blogs.
- Only the author of a blog can modify or delete it.
- Unauthorized users cannot access private blog details.

## Conclusion
This API provides a complete blogging solution with user authentication, blog management, version tracking, and commenting features.

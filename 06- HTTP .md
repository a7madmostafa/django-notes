# HTTP

> Hypertext Transfer Protocol (HTTP) is the foundation of data communication for the World Wide Web. It is an application-layer protocol that enables the transfer of hypertext documents, such as HTML, between a client (usually a web browser) and a server.

## Key Concepts of HTTP
1. **Request-Response Model**: HTTP operates on a request-response model where a client sends an HTTP request to a server, and the server responds with an HTTP response.
2. **Stateless Protocol**: Each HTTP request is independent, meaning that the server does not retain any information about previous requests from the same client. This statelessness simplifies server design but requires mechanisms like cookies or sessions to maintain stateful interactions.
3. **Methods**: HTTP defines several methods that indicate the desired action to be performed on a resource. Common methods include:
   - `GET`: Retrieve data from the server.
   - `POST`: Submit data to be processed to the server.
   - `PUT`: Update a resource on the server.
   - `DELETE`: Remove a resource from the server.
4. **Status Codes**: HTTP responses include status codes that indicate the result of the request. Common status codes include:
   - `200 OK`: The request was successful.
   - `404 Not Found`: The requested resource could not be found.
   - `500 Internal Server Error`: The server encountered an error processing the request.
5. **Headers**: HTTP headers provide additional information about the request or response, such as content type, content length, caching directives, and authentication details.
6. **URLs**: Uniform Resource Locators (URLs) are used to identify resources on the web. They consist of a protocol (e.g., `http` or `https`), a domain name, and a path to the resource.
7. **Cookies**: Cookies are small pieces of data sent from a server to a client and stored on the client's device. They are used for authentication, session management, and other purposes.    
8. **HTTPS**: Hypertext Transfer Protocol Secure (HTTPS) is an extension of HTTP that uses encryption (via SSL/TLS) to secure data transmitted between the client and server, ensuring confidentiality and integrity.

### HTTP Request Example:

```
GET /index.html HTTP/1.1
Host: www.example.com
```
- ***It consists of:***
    - HTTP Method: `GET`
    - Resource Path: `/index.html`
    - HTTP Version: `HTTP/1.1`
    - Headers: `Host: www.example.com`

### HTTP Response Example:

```
HTTP/1.1 200 OK
Content-Type: text/html
<html>
<body>
<h1>Welcome to Example.com!</h1>
</body>
</html>
```
- ***It consists of:***
    - HTTP Version: `HTTP/1.1`
    - Status Code: `200 OK`
    - Headers: `Content-Type: text/html`
    - Body: HTML content of the response

## HTTP in Django
In Django, HTTP is a fundamental part of how web applications are built and interact with users. Django provides a robust framework for handling HTTP requests and responses.

- Django handles the request and response with the help of `HttpRequest` and `HttpResponse` classes in the `django.http` module. 

- Django obtains the `HttpRequest` object from the context provided by the server. 

- As a client request is received, Django’s `URL dispatcher` mechanism invokes a view that matches the URL pattern and passes this `HTTPRequest` object as the first argument so that all the request metadata is available to the view for processing.
# Introduction

The Plateit API follows many standard API conventions, making it easy to understand and use. It supports a variety of operations that allow you to manage resources effectively.

## Methods

The API uses the following HTTP methods to perform operations on resources:

* `GET`: Retrieves a resource or a collection of resource objects.
* `POST`: Creates a new resource (also used by some helper endpoints when no other methods are appropriate).
* `PATCH`: Updates an existing resource.
* `DELETE`: Deletes a resource.

## Errors

The API employs standard HTTP error response codes to communicate issues that may arise during requests (`400`, `401`, `404`, etc). When an error occurs, the response often includes an accompanying `message` string that provides additional context about the error.
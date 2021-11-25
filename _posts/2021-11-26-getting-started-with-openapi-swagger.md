---
layout: post
title: "Getting started with OpenAPI/Swagger"
date: 2021-11-26 08:49:30 +0900
categories: openapi
---

### What is OpenAPI?

OpenAPI is a specification format for documenting APIs. An OpenAPI description of an API will generally consist of one (or more) files (usually in JSON or YAML format) documenting the path and request and response format of each API endpoint. A few different versions of OpenAPI exist, but unless you need to use a tool that only supports older versions, you'll probably want to use the latest (OpenAPI 3.0.3 at the time of writing).

#### Sample OpenAPI v3 definition
```yaml
openapi: '3.0.3'
info:
  title: My API
  description: A sample API
  version: 1.0.0
tags:
  - name: Users
    description: User management
paths:
  /user:
    get:
      operationId: getUser
      summary: Get a user.
      tags:
        - Users
      parameters:
        - in: query
          name: id
          required: true
          description: The user ID.
          schema:
            type: number
            example: 12345
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: number
                    example: 12345
                  name:
                    type: string
                    example: 'John'
              example: { 'id': '12345', 'name': 'John' }
```

### What is Swagger?
Swagger is a set of open-source tools for designing, viewing, and processing OpenAPI specifications. 
[Swagger UI](https://swagger.io/tools/swagger-ui/){:target="\_blank"} is a tool for generating and displaying a nice looking web page based on your OpenAPI specification.<br>
[Swagger Editor](https://swagger.io/tools/swagger-editor/){:target="\_blank"} allows you to edit an OpenAPI specification while viewing its Swagger UI representation side by side for real time feedback.<br>
[Swagger Inspector](https://swagger.io/tools/swagger-inspector/){:target="\_blank"} acts a client to your API and allows you to validate and generate specificationa from your requests and responses.<br>
[Swagger Codegen](https://swagger.io/tools/swagger-codegen/){:target="\_blank"} can generate server and client code from your specification in various languages.

#### SwaggerUI documentation generated from the above definition
![Sample SwaggerUI documentation](/assets/2021-11-26-getting-started-with-openapi-swagger/swaggerui.png)

### Why use OpenAPI/Swagger?
During development the need often arises to reference your API to ensure that you serve and handle requests and responses in the correct format. Without proper documentation, this requires developers to go through the code and piece together the details of the API themselves, slowing down development and potentially introducing bugs, especially if the developer is not familiar with the relevant API code.<br> 
And when exposing a public API for anyone to use and integrate into their products, documentation becomes an absolute necessity. OpenAPI and Swagger allow you to create API documentation in a standard format and publish it, either as the raw specification itself or as an easy to view web page.

### Creating an OpenAPI specification
To get started, you'll first need to create the aforementioned OpenAPI specification in either JSON or YAML format. There are a number of ways to do this.

#### Generation from code comments
There are a number of tools for various languages that can generate an OpenAPI specification for you from comments directly in your source code. This generally requires you to add comments in a specific format to describe the various properties of each endpoint. On the one hand this can clutter up your code with slightly hard to read comments, on the other hand having the definition and code next to each other makes them easy to change together. You'll also need to run a tool to regenerate your specification whenever you make changes but this could of course be automated. <br>
My feeling is that if you're going to learn the specific comment format required by the generation tool you may as well just learn the OpenAPI format and write your specification directly but I can see how generation from comments could be the preferred option for some.

##### Sample of OpenAPI comments in Go from the swaggo library
![Sample OpenAPI comments](/assets/2021-11-26-getting-started-with-openapi-swagger/fromcomments.png)

#### Generation from API calls
[Swagger Inspector](https://swagger.io/docs/swagger-inspector/how-to-create-an-openapi-definition-using-swagger/){:target="\_blank"} is a tool that allows you to generate an OpenAPI specification by sending actual requests to your endpoints and recording the responses. This is quite a neat idea but it does require some extra work such as registering for a Swagger account, setting up the authentication etc. You'll also most likely end up editing the generated specification anyway to add titles and descriptions, fix up type information and so on.

#### Manual creation
Naturally you can also create your specification by hand, and this is the method I currently prefer as the specification format itself is quite readable.  Additionally, the Swagger Editor allows you to validate and view your specification file as you type which is great for beginners. My preference for format is YAML over JSON as the lack of brackets makes it simpler to read and edit, and it also supports comments, which JSON does not.

### Displaying your specification with Swagger UI
Once you have your specification file, you'll want to have it accessible in an easy to read format for others to consume, and this is where Swagger UI comes in. Swagger UI takes your OpenAPI specification and transforms it into a web page that lists your endpoints, their request and response formats along with examples, and even allows you to make actual requests to a test server and view the response. The sample [Pet Store implementation](https://petstore.swagger.io/?_ga=2.98386454.862580301.1636717303-236305632.1636471216){:target="\_blank"} shows how the generated page will look. <br>
Refer to the [official documentation](https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation/){:target="\_blank"} for details on how to get Swagger UI up and running as there are a few different options, but if you're already using Docker the [official Docker image](https://hub.docker.com/r/swaggerapi/swagger-ui){:target="\_blank"} may be the easiest.

### Generating clients and servers
Another somewhat common way to make use of your specification after creating it is to automatically generate client and server code. There are a number of different tools that can generate code in various languages including Swagger's own [Swagger Codegen](https://github.com/swagger-api/swagger-codegen){:target="\_blank"}
This can be a bit hit and miss depening on the language used and generation tool and may require some manual tweaking, but can still be a time saver especially for larger projects.

### Wrapping up
While for small or personal projects the time invested in setting up OpenAPI/Swagger may not be worth the benefits, for large projects with many developers/designers or clients who all need to have confidence in developing for and using your API, it may be worth looking into. <br>
The best way to get a feel or what it's all about is the official sample (Pet Store API)[https://editor.swagger.io/]{:target="\_blank"} where you can play around with the specification and experiment with how changing the various properties affects the generated documentation.

{% include share-buttons.html %}

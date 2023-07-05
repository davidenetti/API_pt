# General considerations about generated docs about API

The overview is typically the first section of API documentation. Generally found at the beginning of the doc, it will provide a high-level introduction to how to connect and use the API. In addition, it could contain information about authentication and rate-limiting.

Review the documentation for functionality, or the actions that you can take using the given API. These will be represented by a combination of an HTTP method (GET, PUT, POST, DELETE) and an endpoint. Every organization’s APIs will be different, but you can expect to find functionality related to user account management, options to upload and download data, different ways to request information, and so on.

When making a request to an endpoint, make sure you note the request requirements. Requirements could include some form of authentication, parameters, path variables, headers, and information included in the body of the request. The API documentation should tell you what it requires of you and mention which part of the request that information belongs in. If the documentation provides examples, use them to help you. Typically, you can replace the example values with the ones you’re looking for.

# Documentation conventions

- : or {} -> The colon or curly brackets are used by some APIs to indicate a path variable. In other words, “:id” represents the variable for an ID number and “{username}” represents the account username you are trying to access;
- [] -> Square brackets indicate that the input is optional;
- || -> Double bars represent different possible values that can be used.

# Collection variables

When you start working with a new collection in Postman it is always a good idea to get a lay of the land, by checking out the collection variables. You can check on your Postman collection variables by using the collection editor.
Make sure that the baseUrl Current Value matches up with the URL to your target.


In order to use Postman to make authorized API requests, we will need to add a valid token to our requests. This can be done for all of the requests within a collection by adding an authorization method to the collection. Using the Authorization tab, within the collection editor, we will need to select the right type for authorization.
Tokens are usually provided after a successful authentication attempt.


# OWASP API 3: Excessive data exposure

Excessive Data Exposure occurs when an API provider sends back a full data object, typically depending on the client to filter out the information that they need. From an attacker's perspective, the security issue here isn't that too much information is sent, instead, it is more about the sensitivity of the sent data. This vulnerability can be discovered as soon as you are able to start making requests. API requests of interest include user accounts, forum posts, social media posts, and information about groups (like company profiles).
Ingredients for excessive data exposure:
- A response that includes more information than what was requested;
- Sensitive Information that can be leveraged in more complex attacks.


If an API provider responds with an entire data object, then the first thing that could tip you off to excessive data exposure is simply the size of the response.


Next we can send some request to different endpoints indentified in the docs and with Burp we can intercept the traffic between the browser and the backend in order to identify potential data exposure.


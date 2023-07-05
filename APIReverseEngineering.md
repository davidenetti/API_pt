# Postman

In Postman create a new workspace in order to save a collection.
Next, start a capture session in postman by enablign a proxy session between the browser and Postman.

When in a target website,  Click on links, register for an account, sign in to the account, visit your profile, post comments in a forum, etc. Essentially click all the things, update information where you can, and explore the web app in its entirety. How thorough you use the web app will have a domino effect on what endpoints and requests you will later test.

Add the captured events to a collection, then create an automatic documentation.

# Automatic documentation

Start mitmweb in order to create a proxy listener using port 8080. next open a browser with FoxyProxy and set the proxy to port 8080 or use Burp Suite.

Next, use the target web application as it was intended.

Save the captured traffic from mitmweb.

We can use the "flows" file to create our own API documentation. Using a great tool called mitmproxy2swagger, we will be able to transform our captured traffic into an Open API 3.0 YAML file that can be viewed in a browser and imported as a collection into Postman.

# mitmproxy2swagger

Run the following:
- `sudo mitmproxy2swagger -i /Downloads/flows -o spec.yml -p http://crapi.apisec.ai -f flow`

After running this you will need to edit the spec.yml file to see if mitmproxy2swagger has ignored too many endpoints. Checking out spec.yml reveals that there are several endpoints that were ignored and the title of the file can be updated.

After running this you will need to edit the spec.yml file to see if mitmproxy2swagger has ignored too many endpoints. Checking out spec.yml reveals that there are several endpoints that were ignored and the title of the file can be updated.
Update the YAML file so that "ignore:" is removed from the endpoints that you want to include. Once you have edited the file it should look something similar to the image below. Note that the "title" has been updated to "crAPI Swagger" and that the endpoints no longer contain "ignore:".


Save the updated spec.yml file and run the mitmproxy2swagger again. This time around add the "--examples" flag to enhance your API documentation.

After running mitmproxy2swagger successfully a second time through, your reverse-engineered documentation should be ready. You can validate the documentation by visiting https://editor.swagger.io/ and by importing your spec file into the Swagger Editor. Use File>Import file and select your spec.yml file. If everything has gone as planned then you should see something like the image below. This is a pretty good indication of success, but to be sure we can also import this file as a Postman Collection that way we can prepare to attack the target API.


# Import final OpenAPI generated docs to Postman

To import this file as a collection we will need to open Postman. At the top left of your Postman Workspace, you can click the "Import" button. Next, select the spec.yml file and import the collection.

Once you import the file you should see a relatively straightforward API collection that can be used to analyze the target API and exploit with future attacks.

With a collection prepared, you should now be ready to use the target API as it was designed. This will enable you to see the various endpoints and understand what is required to make successful requests. In the next module, we will get begin working with the API and learn to analyze various requests and responses. 
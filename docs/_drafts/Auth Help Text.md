## Basic

### Step 1: Configure a Test Request & Connection Label

The only things to needed for Basic auth are a test API call to verify users' credentials, and a connection label to identify accounts. Zapier automatically configures everything else, and includes the username and password in API calls automatically.

### _Connection Label_ (want a custom one here to point out how to use the username field.)

Customize the connection label to help users differentiate between app accounts. Include {{bundle.authData.username}} to include the username, or {{bundle.inputData.field}} to reference fields from your Test API call, replacing field with the field name to use in the label. <a href="https://platform.zapier.com/docs/auth#label" target="_blank" >Learn More</a>'





## Session

### Step 1: Configure your Fields

Build a form with fields for each item your API requires for authentication, such as username, password, subdomain, and more. Zapier does not include any field by default. <a href="https://platform.zapier.com/docs/session#form" target="_blank" >Learn More</a>'

### Step 2: Configure a Token Exchange Request

Enter your Token Exchange URL where Zapier can exchange user credentials for the token. Zapier automatically includes the data from your input form in the request body; click _Show Options_ to customize the API call, and type `{{` in any value field to see bundle data field options. <a href="https://platform.zapier.com/docs/session#access" target="_blank" >Learn More</a>'

### Step 3: Configure Test Request & Connection Label

Add a simple API endpoint to test user credentials. Include the token in the URL Params or HTTP Headers as required by your API with `{{bundle.authData.accessToken}}`, replacing `accessToken` with your API's field name for the token. <a href="https://platform.zapier.com/docs/session#test" target="_blank" >Learn More</a>'





## API Key

### Step 1: Configure your Fields

Build a form with fields for each item your API requires for authentication, including a field for your API key and additional field for any other data needed. Zapier does not include any fields by default. <a href="https://platform.zapier.com/docs/apikey#form" target="_blank" >Learn More</a>'

### Step 2: Configure a Test Request and Connection Label

Add a simple API endpoint to test user credentials. Zapier includes data from your input form in the URL Params by default; click _Show Options_ to customize the API call if your API expects them in the header instead. <a href="https://platform.zapier.com/docs/apikey#request" target="_blank" >Learn More</a>'





## OAuth v2

### Step 1: Configure your Fields

If your API's OAuth Authorization URL does not require details about the user, click _Continue_ to skip this step. Otherwise, add input fields for each item—such as subdomain or team name—that your API requires to show the Authorization page.  <a href="https://platform.zapier.com/docs/oauth#form" target="_blank" >Learn More</a>'

### Step 2: Copy your OAuth Redirect URL

Copy the link below, then use it in your app's API or developer settings to create a new integration or app to use with Zapier. <a href="https://platform.zapier.com/docs/oauth#redirect" target="_blank" >Learn More</a>'

### Step 3: Enter your Application Credentials

From your app's API or developer settings, copy the Client ID and Secrete from your app and paste them below. <a href="https://platform.zapier.com/docs/oauth#credentials" target="_blank" >Learn More</a>'


### Step 4: OAuth v2 Endpoint Configuration

Add the Authorization URL from your API—no additional settings are typically needed—optionally with comma-separated scopes. Then add your API's Access Token request and refresh endpoints. Zapier includes the default fields, though click _Show options_ to customize if needed. Finally add a test API call to test your authentication, and a connection label to identify accounts. <a href="https://platform.zapier.com/docs/oauth#authorization" target="_blank" >Learn More</a>'





## Digest

### Step 1: Configure your Fields

Zapier automatically includes a form to request usernames and passwords for authentication with Digest Auth. If your API requires additional fields, add them here. Otherwise, continue to Step 2.  <a href="https://platform.zapier.com/docs/digest#form" target="_blank" >Learn More</a>'

### Step 2: Configure a Test Request and Connection Label

Add a simple API endpoint to test user credentials. Click _Show Options_ to customize the data Zapier sends your API call, and type `{{` in any value field to see bundle data field options. <a href="https://platform.zapier.com/docs/digest#test" target="_blank" >Learn More</a>'
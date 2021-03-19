# Social-Login - Asset

**Social login enables users to log in to React store by using a social networking account, rather than using credentials dedicated to HCL Commerce which will make the sign up and login process quicker**

**DISCLAIMER:  This asset is being provided as-is to help accelerate your projects.  As such, we are unable to provide official support for this asset.  We have provided documentation as well as any needed code artifacts for your use.**

**Prerequisites:** HCL Commerce V9.1.x / HCL Commerce React Storefront SDK



In Social Login, below two options are implemented

    1. Login With Google
    2. Login With Facebook
    
**The implemntation includes below steps**
 1.	Create a social networking app for HCL Commerce on both Google and Facebook
 2.	Register your app in your STORECONF table
 3.	Create UI components for Social Login buttons and get the success response of the OAuth server and make a call to POST query “/store/{storeId}/loginidentity/oauth_validate” for authorization.

### Step-1: Create a social networking app for HCL Commerce on both Google and Facebook

**Google Sign in**

    •	Open the Google API Console 
    •	Open Credentials page.
    •	From the project drop-down, select an existing project or create a new one.
    •	On the Credentials page, select Create credentials, then select OAuth client ID.
    •	Under Application type, choose Web application.
    •	Click Create.
    •	Get the Client ID and Client Secret ID.

**Facebook Sign In**

    •	Go to the Facebook for Developers page and login with your Facebook account.
    •	At the right corner of the top navigation bar, click the My Apps link and select Add New App.
    •	Enter the Display Name and Contact Email.
    •	Click the Create App ID button.
    •	The new App will be created and redirected to the Facebook App Dashboard.
    •	Navigate to the Settings » Basic page.
    •	In App Domains field, specify the domain name of your website (ex: emerald.com).
    •	In Privacy Policy URL field, specify the privacy policy web page URL for login dialog 
    •	Select the Category of your App.
    •	Click the Save Changes button.
    •	Get the App ID and App Secret ID.

### Step-2: Register your app in your STORECONF table in DB

**Google**

    //Specify the field name that we will use for provider
    insert into STORECONF values (<store_id>, 'Google.oauth.clientIdField', 'client_id', 0);
    insert into STORECONF values (<store_id>, 'Google.oauth.clientSecretField', 'client_secret', 0);

    //Provide the values of the fields you specified above
    insert into STORECONF values (<store_id>, 'Google_client_id', ‘<YOUR GOOGLE CLIENT ID>’, 0);
    insert into STORECONF values (<store_id>, 'Google_client_secret', '<YOUR GOOGLE SECRET ID>', 0);

    //Provide the OAuth server URL which will verify the token and provide the parameter name “accesstoken”
    insert into STORECONF values (<store_id>',Google_provider_verifytoken_url', ‘https://oauth2.googleapis.com/tokeninfo’, 0);
    insert into STORECONF values (<store_id>,'Google.oauth.verifiedTokenField', 'access_token', 0);


**Facebook**

    //Specify the field name that we will use for provider
    insert into STORECONF values (<store_id>, 'Facebook.oauth.clientIdField', 'appId', 0);
    insert into STORECONF values (<store_id>, 'Facebook.oauth.clientSecretField', 'appSecret', 0);

    //Provide the values of the fields you specified above
    insert into STORECONF values (<store_id>, 'Facebook_appId', ‘<YOUR FACEBOOK APP ID>’, 0);
    insert into STORECONF values (<store_id>, 'Facebook_appSecret', ‘<YOUR FACEBOOK APP SECRET ID>’, 0);

    //Provide the OAuth server URL which will verify the token and provide the parameter name “inputtoken”
    insert into STORECONF values (<store_id>, 'Facebook_provider_verifytoken_url', 'https://graph.facebook.com/debug_token', 0);
    insert into STORECONF values (<store_id>, 'Facebook.oauth.verifiedTokenField', 'input_token', 0);


### Step:3 Create UI components for Social Login buttons

**Google**
 
1. You need to install the react-google-login in your project as a dependency.

   `npm install react-google-login`
 
2.  Replace the <YOUR_GOOGLE_CLIENT_ID> with your Google client ID in GoogleSignIn.tsx file.

**Facebook**

1. You need to install the react-facebook-login in your project as a dependency.

   `npm install react-facebook-login`
 
2.  Replace the <YOUR_FACEBOOK_APP_ID> with your Facebook App Id in FacebookSignIn.tsx  file.


Once done with the changes then import these components in SignInLayout.tsx file and use it as below

        <GoogleSignIn />
        <FacebookSignIn />
 
 
 
 

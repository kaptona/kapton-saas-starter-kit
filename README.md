# Kapton's SaaS Starter Kit
*A SaaS boilerplate written in Next.js, Firebase (and Firestore), Xkit and Chakra UI.*

**Preview here:** https://saas-starter.vercel.app/ 

## How to setup

#### Getting the repository

1. Download/clone the repository.
    
    `git clone https://github.com/kaptona/kapton-saas-starter-kit`

#### Installing the required packages

2. Go to the downloaded/cloned folder and install the dependencies using:
    
    `npm install` or `yarn install`

#### Setting up the .env.local file

3. Find the *.env.local.sample* file and rename it to *.env.local*.

#### Setting up Firebase

4. Create a Firebase account [here](https://firebase.google.com/).

5. Go to the Firebase console and create an app by clicking on *Add app*.

6. Set up *Authentication* and *Cloud Firestore*.

7. Go to the Firebase project settings and find the Firebase SDK config details under *Your apps*.

8. Open the *.env.local* file and put the Firebase SDK config details there like so:

       NEXT_PUBLIC_FIREBASE_API_KEY=<put_api_key_here>
       NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=<put_auth_domain_here>
       NEXT_PUBLIC_FIREBASE_PROJECT_ID=<put_project_id_here>
       NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=<put_storage_bucket_here>
       NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=<put_messaging_sender_id>
       NEXT_PUBLIC_FIREBASE_APP_ID=<put_app_id_here>
        
9. Go to Firebase project settings and click on *Service Accounts*.<br>
Then on Firebase Admin SDK, *Create service account* and generate new private key. Drag and drop the downloaded file in the project folder.<br>
Rename the file to *firebase-key.json*

10. Still on the *Service Accounts* tab, find *databaseURL* and paste it in *.env.local* like so: 

        NEXT_PUBLIC_FIREBASE_DATABASE_URL=<put_database_url_here>

#### Setting up Firestore
11. Go to the Firebase console, open the  *Cloud Firestore* tab and click on *Rules*. Then copy-paste this there:
        
        rules_version = '2';
        service cloud.firestore {
          match /databases/{database}/documents {
            match /{document=**} {
              allow read, write: if request.auth != null;
            }
          }
        }
        
    While these rules are valid, they are not recommended for production applications.<br>
    You can check out [security rules](https://firebase.google.com/docs/firestore/security/get-started) to learn more.

#### Setting up Xkit

12. Create an Xkit account [here](https://xkit.co/).

13. Go to the *New Connector* tab and install a connector/s.

14. Go to the *Settings* tab, scroll down to *API Keys*, and click on *Generate API Key*. 

15. Open the *.env.local* file and put the Xkit Publishable Key, Secret Key and URL Slug (you can find it on the settings page) like this:
        
        NEXT_PUBLIC_XKIT_PUBLISHABLE_KEY=<put_publishable_key_here>
        NEXT_PUBLIC_XKIT_SECRET_KEY=<put_secret_key_here>
        NEXT_PUBLIC_XKIT_DOMAIN=<put_url_slug_here>
        
16. On the *Settings* tab go to *Valid Web Origins* and add *http://localhost:3000*.

17. Still on *Settings* go to *User Tokens* and click on *Add Custom Issuer*.<br>
For the *iss Claim*, use the value https://securetoken.google.com/{projectId} where {projectId} is the Firebase project ID, the unique identifier for your Firebase project, which can be found in the URL of that project's console.<br>
For the *aud Claim*, use the {projectId} value.<br>
For the *User ID Claim*, keep it as *sub*.<br>
For the *JSON Web Key Set URL*, use the value https://www.googleapis.com/service_accounts/v1/jwk/securetoken@system.gserviceaccount.com
        
### Hooray, that was all!<br>
To view the result, run `npm run dev` in the project folder and go to http://localhost:3000.

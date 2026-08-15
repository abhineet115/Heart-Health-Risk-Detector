# 🔒 Security Guide: Protecting Your Firebase API & Database

In client-side (frontend) web applications, Firebase API keys are identifiers used by the Firebase SDK to route traffic to your project. To prevent unauthorized use, quota theft, or data tampering, you must enforce security at three distinct layers:

1. **API Key Restrictions** (Google Cloud Console)
2. **Authorized Domains** (Firebase Console)
3. **Firestore Security Rules** (`firestore.rules`)
4. **Firebase App Check** (Optional but Recommended)

---

## 1. 🛡️ Restrict Your Firebase API Key in Google Cloud Console

By restricting your API key, you ensure that **only your authorized website domains** can use the API key, and it can only call the necessary Firebase services.

### Step-by-Step Instructions:

1. Open the [Google Cloud Console Credentials Page](https://console.cloud.google.com/apis/credentials).
2. Select your Firebase project (e.g. `<your-project-id>`).
3. Under **API Keys**, locate the key corresponding to your web app (starts with `AIzaSy...`).
4. Click the pencil/edit icon ✏️ to modify the key.

### A. Set Application Restrictions (HTTP Referrers)
1. Under **Application restrictions**, select **Websites**.
2. Under **Website restrictions**, click **ADD**:
   - `http://localhost:*`
   - `http://127.0.0.1:*`
   - `https://<your-username>.github.io/*`
   - `https://<your-project-id>.firebaseapp.com/*`
   - `https://<your-project-id>.web.app/*`

### B. Set API Restrictions
1. Under **API restrictions**, select **Restrict key**.
2. In the dropdown, check only the required APIs for this project:
   - ✅ **Identity Toolkit API** *(Required for Firebase Auth)*
   - ✅ **Token Service API** *(Required for Auth tokens)*
   - ✅ **Cloud Firestore API** *(Required for Firestore Database)*
   - ✅ **Firebase Installations API**
3. Click **Save**.

---

## 2. 🌐 Configure Authorized Domains in Firebase Console

Ensure that OAuth sign-in providers (such as Google Sign-In) only accept requests originating from your verified domains.

1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Open your project.
3. Navigate to **Build** > **Authentication** > **Settings** tab.
4. Click on **Authorized domains**.
5. Ensure only your approved domains are listed:
   - `localhost`
   - `<your-project-id>.firebaseapp.com`
   - `<your-project-id>.web.app`
   - `<your-username>.github.io`

---

## 3. 📑 Enforce Firestore Database Security Rules

Firestore security rules run on Google's servers and validate every single read, write, and delete operation before it touches your database.

The repository includes a ready-to-use [`firestore.rules`](firestore.rules) file.

### How to apply in Firebase Console:
1. Go to [Firebase Console](https://console.firebase.google.com/) > **Firestore Database**.
2. Click the **Rules** tab at the top.
3. Paste the contents of [`firestore.rules`](firestore.rules):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Default deny all access
    match /{document=**} {
      allow read, write: if false;
    }

    // Secure user health records
    match /artifacts/{appId}/users/{userId}/healthRecords/{recordId} {
      // Allow read/write only if the authenticated user matches the userId
      allow read, update, delete: if request.auth != null && request.auth.uid == userId;

      // Validate schema on document creation
      allow create: if request.auth != null 
                    && request.auth.uid == userId
                    && request.resource.data.keys().hasAll(['score', 'level', 'age', 'gender'])
                    && request.resource.data.score is number
                    && request.resource.data.score >= 0 
                    && request.resource.data.score <= 60
                    && request.resource.data.age is number
                    && request.resource.data.age >= 1 
                    && request.resource.data.age <= 120;
    }

    // Secure top-level user records
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

4. Click **Publish**.

---

## 4. 🛡️ Enable Firebase App Check (Advanced Protection)

Firebase App Check uses **reCAPTCHA Enterprise** or **reCAPTCHA v3** to ensure that requests originate only from real users interacting with your verified web app, blocking automated bot traffic and unauthorized API scrapers.

1. Go to **Firebase Console** > **App Check**.
2. Register your web app with **reCAPTCHA Enterprise** or **reCAPTCHA v3**.
3. Enforce App Check on **Cloud Firestore** and **Authentication**.

# Mobile Otp Authentications

# Firebase

* Firebase is a Backend-as-a-Service, and it is a real-time database which is basically designed for mobile applications.
* Google Firebase is a Google-backed application development software that enables developers to develop iOS,Android and 
Web apps. Firebase provides tools for tracking analytics,reporting and fixing app crashes,creating marketing and product
experiment.

![firebase](https://user-images.githubusercontent.com/51777024/85911219-814e5180-b841-11ea-8071-273f9b78c4f9.png)

# Features of Firebase
Firebase has several features that make this platform essential. These features include unlimited reporting, cloud messaging,
authentication and hosting, etc. Let's take a look at these features to understand how these features make Firebase essential.

![Bg4r7dI1Q2W3bX9Sf4oD_unnamed](https://user-images.githubusercontent.com/51777024/85911120-9d9dbe80-b840-11ea-873f-f30665d098ff.png)

# Firebase Authentication

* Authentication is the process of recognizing a user’s identity. 
* It is the mechanism of associating an incoming request with a set of identifying credentials. 
* The credentials are maintained authentication server.
* Mobile authentication is the verification of a user's identity through the use a mobile device and one or more authentication 
  methods for secure access.

![firebase-authentication](https://user-images.githubusercontent.com/51777024/85911439-d9398800-b842-11ea-99ef-9c5631ddb172.png)

# Types of Authentications

You can authenticate your app’s users through the following methods:

* Email & Password
* Phone numbers
* Google
* Facebook
* Twitter

![pasted image 0](https://user-images.githubusercontent.com/51777024/85911863-93ca8a00-b845-11ea-87ae-cd5ef11a840d.png)

# Sample Mobile Otp Authentication

![example](https://user-images.githubusercontent.com/51777024/85912071-35061000-b847-11ea-86fb-3a27ac3c92a6.jpg)

# Steps to Implementation Of Application

We create a new project by clicking on Start a new Android Studio project from Welcome to Android Studio dialog box.

![imag1](https://user-images.githubusercontent.com/51777024/85912182-400d7000-b848-11ea-81ec-e523965e1fae.jpg)

![image2](https://user-images.githubusercontent.com/51777024/85912231-9084cd80-b848-11ea-9595-56625b09fc58.png)

![image3](https://user-images.githubusercontent.com/51777024/85912239-a5616100-b848-11ea-8a43-03d311d44df3.png)

# Firebase Assistance

We can simply add Firebase using Firebase Assistance by selecting Firebase from the tools menu in Android Studio
When we click on Firebase, a new window will open that contains several Firebase features such as Analytics, Cloud
Messaging, Authentication,and Real-time Database, etc.

![f1](https://user-images.githubusercontent.com/51777024/85912347-78617e00-b849-11ea-949d-ecba0a0b447b.png)

Let's start with basics, i.e., Analytics. When we select Analytics, it gives us the step by step guide of what we need to do.

![f2](https://user-images.githubusercontent.com/51777024/85912353-7f888c00-b849-11ea-99e4-9bc3e1ca528a.png)

Step 1:

So, in the first step, we will connect to Firebase. When we click on connect to Firebase, it may bring up our browser, and wemay have to log into our Google account.If we log in to our Google account, 
we may have to give access to Android Studio so that it can allow us to add stuff.

![f3](https://user-images.githubusercontent.com/51777024/85912357-86af9a00-b849-11ea-8712-b9f4bf0fe118.png)

When we click on allow, it will take us back to Android Studio. Because our project is already connected with Firebase, it will pop up a message, i.e., Firebase already connected. But if our project is not connected with Firebase, it will show the following window.

![f4](https://user-images.githubusercontent.com/51777024/85912364-8c0ce480-b849-11ea-8d3b-8c6263261c96.png)

Here, we have to create a new Firebase project or choosing the existing Firebase project. It completely depends on us. When we click on Connect to Firebase, our project will connect with Firebase successfully.

![f5](https://user-images.githubusercontent.com/51777024/85912367-8fa06b80-b849-11ea-8bd4-844f90d5aa53.png)

Step 2:

In the next step, we will add analytics to our app by clicking on Add Analytics to your app. This will actually update our build.gradle files, which we did in the previous section.

![f6](https://user-images.githubusercontent.com/51777024/85912370-9202c580-b849-11ea-9d4c-050d9743335f.png)

When we click on Accept Changes, it will update our Gradle files, which we can verify by going to build. Gradle files.

![f7](https://user-images.githubusercontent.com/51777024/85912372-962ee300-b849-11ea-9077-e3a46ba7a437.png)

![f8](https://user-images.githubusercontent.com/51777024/85912373-9929d380-b849-11ea-848c-912f425b58c0.png)

Step 3:

To sign in users by SMS, you must first enable the Phone Number sign-in method for your Firebase project:
* In the Firebase console, open the Authentication section.
* On the Sign-in Method page, enable the Phone Number sign-in method.

Step 4 :get the firebase instance at oncreate()

```
private FirebaseAuth mAuth;
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```
Step 5: Send a Verification Code to the Users Phone

```
pass their phone number to the PhoneAuthProvider.verifyPhoneNumber method to request that Firebase verify the user's phone number.

PhoneAuthProvider.getInstance().verifyPhoneNumber(
        phoneNumber,        // Phone number to verify
        60,                 // Timeout duration
        TimeUnit.SECONDS,   // Unit of timeout
        this,               // Activity (for callback binding)
        mCallbacks);        // OnVerificationStateChangedCallbacks
```
Step6 : implementation on callback functions

```
mCallbacks = new PhoneAuthProvider.OnVerificationStateChangedCallbacks() {@Override
    public void onVerificationCompleted(PhoneAuthCredential credential) 
   {      
Log.d(TAG, "onVerificationCompleted:" + credential);
 signInWithPhoneAuthCredential(credential);
    }
@Override
    public void onVerificationFailed(FirebaseException e) 
  {
          
    }

```
Step7 :implementation on callback functions

```
 @Override
    public void onCodeSent(@NonNull String verificationId,
                           @NonNull PhoneAuthProvider.ForceResendingToken token) {
            Log.d(TAG, "onCodeSent:" + verificationId);
        // Save verification ID and resending token so we can use them later
        mVerificationId = verificationId;
        mResendToken = token
        // ...
    }
};

```
Step8 :Create the PhoneAuthCredential Object

```
To create the PhoneAuthCredential object, call PhoneAuthProvider.getCredential
PhoneAuthCredential credential = PhoneAuthProvider.getCredential(verificationId, code);

```

Step 9: Signin with User

```
private void signInWithPhoneAuthCredential(PhoneAuthCredential credential) 
{
    mAuth.signInWithCredential(credential).addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
           @Override
           public void onComplete(@NonNull Task<AuthResult> task){
           if (task.isSuccessful()) 
          {
           //navigate new activity                                    
          } else 
          {
              //failed      
          }
          }
          }
            });}
            
```

# Firebase: Google Sign-In Authentication

As we have discussed earlier, Firebase provides different types of Authentication methods. In our previous section, we learned how authentication is done using Firebase UI and Firebase SDK. In this section, we will learn another method, i.e., Google Sign-in Authentication. It is pretty easy to do.

Starting steps are the same as we have done with other authentication methods, which are as follows:

Creating an Android project.
Creating a Firebase project.
Adding Firebase to the Android project or application, either manually or Firebase Assistance.
Adding the required libraries and JSON files.

# Step 1:

Apart from firebase auth and core libraries, we have to add google play services auth in app.gradle file

![s1](https://user-images.githubusercontent.com/51777024/85913133-a944b180-b84f-11ea-93ae-6eb869d4a702.png)

# Step 2:

In the next step, we have to enable the Google sign-in method in Firebase console. We also have to add a project supporting email.

![s2](https://user-images.githubusercontent.com/51777024/85913134-ad70cf00-b84f-11ea-8ae1-a7d3ffa6c374.png)

# Step 3:

Just like our previous method, we have to set SHA-1 and SHA-256 keys.

![s3](https://user-images.githubusercontent.com/51777024/85913135-b2358300-b84f-11ea-80b3-744873b971f6.png)

# Step 4:

In the next step, we will create the layout file that contains three buttons Google sign-in, sign-out, and sign-out and disconnect. The activity layout will look like:

![s4](https://user-images.githubusercontent.com/51777024/85913138-b661a080-b84f-11ea-92c2-c72b01232c78.png)

# Step 5:

Now, we will modify our MainActivity.java file to perform the Google sign-in authentication in the following way:

```
//Implement OnClickListener for sign-in button   
public class MainActivity extends AppCompatActivity implements View.OnClickListener {  
  
    //Adding tag for logging and RC_SIGN_IN for an activity result  
private static final String TAG = "GoogleActivity";  
private static final int RC_SIGN_IN = 9001;  
  
    // Adding Google sign-in client  
    GoogleSignInClient mGoogleSignInClient;  
  
    //Creating member variable for FirebaseAuth  
private FirebaseAuth mAuth;  
  
    @Override  
protected void onCreate(Bundle savedInstanceState) {  
super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        //Adding buttons to the OnClickListener  
        findViewById(R.id.sign_in_button).setOnClickListener(this);  
        findViewById(R.id.signOutButton).setOnClickListener(this);  
        findViewById(R.id.disconnectButton).setOnClickListener(this);  
  
        //Building Google sign-in and sign-up option.  
// Configuring Google Sign In  
GoogleSignInOptions gso = new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)  
// for the requestIdToken, use getString(R.string.default_web_client_id), this is in the values.xml file that  
                // is generated from your google-services.json file (data from your firebase project), uses the google-sign-in method  
                // web api key  
.requestIdToken(getString(R.string.default_web_client_id))//Default_web_client_id will be matched with the   
                .requestEmail()  
                .build();  
  
// Build a GoogleSignInClient with the options specified by gso.  
mGoogleSignInClient = GoogleSignIn.getClient(this, gso);  
  
// Set the dimensions of the sign-in button.  
SignInButton signInButton = findViewById(R.id.sign_in_button);  
        signInButton.setSize(SignInButton.SIZE_WIDE);  
  
// Initialize Firebase Auth  
mAuth = FirebaseAuth.getInstance();  
    }  
     //Creating onStart() method.  
    @Override  
public void onStart() {  
super.onStart();  
  
// Checking if the user is signed in (non-null) and update UI accordingly.  
FirebaseUser currentUser = mAuth.getCurrentUser();  
  
if (currentUser != null) {  
            Log.d(TAG, "Currently Signed in: " + currentUser.getEmail());  
            Toast.makeText(MainActivity.this, "Currently Logged in: " + currentUser.getEmail(), Toast.LENGTH_LONG).show();  
        }  
    }  
     //Calling onActivityResult to use the information about the sign-in user contains in the object.  
    @Override  
public void onActivityResult(int requestCode, int resultCode, Intent data) {  
super.onActivityResult(requestCode, resultCode, data);  
  
// Result returned from launching the Intent from GoogleSignInApi.getSignInIntent(...);  
if (requestCode == RC_SIGN_IN) {  
            Task<GoogleSignInAccount> task = GoogleSignIn.getSignedInAccountFromIntent(data);  
try {  
// Google Sign In was successful, authenticate with Firebase  
GoogleSignInAccount account = task.getResult(ApiException.class);  
                Toast.makeText(this, "Google Sign in Succeeded",  Toast.LENGTH_LONG).show();  
                firebaseAuthWithGoogle(account);  
            } catch (ApiException e) {  
// Google Sign In failed, update UI appropriately  
Log.w(TAG, "Google sign in failed", e);  
                Toast.makeText(this, "Google Sign in Failed " + e,  Toast.LENGTH_LONG).show();  
            }  
        }  
    }  
    //Creating helper method FirebaseAuthWithGoogle().    
private void firebaseAuthWithGoogle(GoogleSignInAccount acct) {  
        Log.d(TAG, "firebaseAuthWithGoogle:" + acct.getId());  
        //Calling get credential from the oogleAuthProviderG  
        AuthCredential credential = GoogleAuthProvider.getCredential(acct.getIdToken(), null);  
mAuth.signInWithCredential(credential)  
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {  
//Override th onComplete() to see we are successful or not.   
 @Override  
public void onComplete(@NonNull Task<AuthResult> task) {  
if (task.isSuccessful()) {  
// Update UI with the sign-in user's information  
FirebaseUser user = mAuth.getCurrentUser();  
                            Log.d(TAG, "signInWithCredential:success: currentUser: " + user.getEmail());  
                            Toast.makeText(MainActivity.this, "Firebase Authentication Succeeded ",  Toast.LENGTH_LONG).show();  
                        } else {  
// If sign-in fails to display a message to the user.  
Log.w(TAG, "signInWithCredential:failure", task.getException());  
                            Toast.makeText(MainActivity.this, "Firebase Authentication failed:" + task.getException(),  Toast.LENGTH_LONG).show();  
                        }  
                    }  
                });  
    }  
  
public void signInToGoogle(){  
        //Calling Intent and call startActivityForResult() method   
        Intent signInIntent = mGoogleSignInClient.getSignInIntent();  
        startActivityForResult(signInIntent, RC_SIGN_IN);  
    }  
  
private void signOut() {  
// Firebase sign out  
FirebaseAuth.getInstance().signOut();  
  
// Google sign out  
mGoogleSignInClient.signOut().addOnCompleteListener(this,  
new OnCompleteListener<Void>() {  
                    @Override  
public void onComplete(@NonNull Task<Void> task) {  
// Google Sign In failed, update UI appropriately  
Toast.makeText(getApplicationContext(),"Signed out of google",Toast.LENGTH_SHORT).show();  
                    }  
                });  
    }  
  
private void revokeAccess() {  
// Firebase sign out  
FirebaseAuth.getInstance().signOut();  
  
// Google revoke access  
mGoogleSignInClient.revokeAccess().addOnCompleteListener(this,  
new OnCompleteListener<Void>() {  
                    @Override  
public void onComplete(@NonNull Task<Void> task) {  
// Google Sign In failed, update UI appropriately  
Log.w(TAG, "Revoked Access");  
                    }  
                });  
    }  
  
    @Override  
public void onClick(View v) {  
int i = v.getId();  
if (i == R.id.sign_in_button) {  
Adding signInToGoogle() method  
 signInToGoogle();  
        }  
else if (i == R.id.signOutButton) {  
            signOut();  
        }  
else if (i == R.id.disconnectButton) {  
            revokeAccess();  
        }  
    }  
  
    @Override  
public void onPointerCaptureChanged(boolean hasCapture) {  
  
    }  
}  
```

![s5](https://user-images.githubusercontent.com/51777024/85913140-ba8dbe00-b84f-11ea-9b8a-424b6270ad96.png)

![s6](https://user-images.githubusercontent.com/51777024/85913142-bd88ae80-b84f-11ea-81bb-ba6a28dd4ec8.png)


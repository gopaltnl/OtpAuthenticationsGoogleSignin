# Firebase Mobile Otp Authentication

# Firebase

* Firebase is a Backend-as-a-Service, and it is a real-time database which is basically designed for mobile applications.
* Google Firebase is a Google-backed application development software that enables developers to develop iOS,Android and Web apps. 
* Firebase provides tools for tracking analytics,reporting and fixing app crashes,creating marketing and product experiment.

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

# Step 1:

So, in the first step, we will connect to Firebase. When we click on connect to Firebase, it may bring up our browser, and wemay have to log into our Google account.If we log in to our Google account, 
we may have to give access to Android Studio so that it can allow us to add stuff.

![f3](https://user-images.githubusercontent.com/51777024/85912357-86af9a00-b849-11ea-8712-b9f4bf0fe118.png)

When we click on allow, it will take us back to Android Studio. Because our project is already connected with Firebase, it will pop up a message, i.e., Firebase already connected. But if our project is not connected with Firebase, it will show the following window.

![f4](https://user-images.githubusercontent.com/51777024/85912364-8c0ce480-b849-11ea-8d3b-8c6263261c96.png)

Here, we have to create a new Firebase project or choosing the existing Firebase project. It completely depends on us. When we click on Connect to Firebase, our project will connect with Firebase successfully.

![f5](https://user-images.githubusercontent.com/51777024/85912367-8fa06b80-b849-11ea-8bd4-844f90d5aa53.png)

# Step 2:

In the next step, we will add analytics to our app by clicking on Add Analytics to your app. This will actually update our build.gradle files, which we did in the previous section.

![f6](https://user-images.githubusercontent.com/51777024/85912370-9202c580-b849-11ea-9d4c-050d9743335f.png)

When we click on Accept Changes, it will update our Gradle files, which we can verify by going to build. Gradle files.

![f7](https://user-images.githubusercontent.com/51777024/85912372-962ee300-b849-11ea-9077-e3a46ba7a437.png)

![f8](https://user-images.githubusercontent.com/51777024/85912373-9929d380-b849-11ea-848c-912f425b58c0.png)

# Step 3:

To sign in users by SMS, you must first enable the Phone Number sign-in method for your Firebase project:
* In the Firebase console, open the Authentication section.
* On the Sign-in Method page, enable the Phone Number sign-in method.

# Step 4: activity_main.xml file

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:hint="Enter Valid Phone No"
        android:inputType="phone"
        android:id="@+id/phone"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="sendotp"
        android:id="@+id/sendotp"
        />
   <EditText
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Enter Otp Here"
       android:id="@+id/otp"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="signin"
        android:id="@+id/sendsignin"/>
</LinearLayout>
```
# Step 5:create the methods and get the id edittext 

```
package com.example.gopalotpauth;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.android.gms.tasks.TaskExecutors;
import com.google.firebase.FirebaseException;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseAuthInvalidCredentialsException;
import com.google.firebase.auth.PhoneAuthCredential;
import com.google.firebase.auth.PhoneAuthProvider;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    EditText phone,otp;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
       
        phone=findViewById(R.id.phone);
        otp=findViewById(R.id.otp);

        findViewById(R.id.sendotp).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

              
            }

          
        findViewById(R.id.sendsignin).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

               
            }
    }
}


```

# Step 6 :get the firebase instance at oncreate()

```
private FirebaseAuth mAuth;
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```
# Step 7: Send a Verification Code to the Users Phone

```
pass their phone number to the PhoneAuthProvider.verifyPhoneNumber method to request that Firebase verify the user's phone number.

PhoneAuthProvider.getInstance().verifyPhoneNumber(
        phoneNumber,        // Phone number to verify
        60,                 // Timeout duration
        TimeUnit.SECONDS,   // Unit of timeout
        this,               // Activity (for callback binding)
        mCallbacks);        // OnVerificationStateChangedCallbacks
```
# Step 8: implementation on callback functions

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
# Step 9 :implementation on callback functions

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
# Step 10:Create the PhoneAuthCredential Object

```
To create the PhoneAuthCredential object, call PhoneAuthProvider.getCredential
PhoneAuthCredential credential = PhoneAuthProvider.getCredential(verificationId, code);

```

# Step 11: Signin with User

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
# Step 12: MainActivity.java file

```
package com.example.gopalotpauth;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.android.gms.tasks.TaskExecutors;
import com.google.firebase.FirebaseException;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseAuthInvalidCredentialsException;
import com.google.firebase.auth.PhoneAuthCredential;
import com.google.firebase.auth.PhoneAuthProvider;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    EditText phone,otp;
    FirebaseAuth auth;
    String vid;
    private PhoneAuthProvider.ForceResendingToken mResendToken;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        auth=FirebaseAuth.getInstance();
        phone=findViewById(R.id.phone);
        otp=findViewById(R.id.otp);

        findViewById(R.id.sendotp).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                sendotpauth();
            }

            private void sendotpauth()
            {
                String ph=phone.getText().toString();
                if (ph.isEmpty())
                {
                    phone.setError("PHONE NO IS REQUIRED");
                    phone.requestFocus();
                    return;
                }
                if (phone.length()<10)
                {
                    phone.setError("ENTER VALID PHONE NUMBER");
                    phone.requestFocus();
                    return;
                }
                PhoneAuthProvider.getInstance().verifyPhoneNumber(ph,60,
                        TimeUnit.SECONDS, TaskExecutors.MAIN_THREAD,mcallback);
            }

            PhoneAuthProvider.OnVerificationStateChangedCallbacks mcallback=new
                    PhoneAuthProvider.OnVerificationStateChangedCallbacks() {

                        @Override
                        public void onCodeSent(String s, PhoneAuthProvider.ForceResendingToken forceResendingToken) {
                            super.onCodeSent(s, forceResendingToken);
                            vid=s;

                        }

                        @Override
                        public void onVerificationCompleted(PhoneAuthCredential phoneAuthCredential) {

                        }

                        @Override
                        public void onVerificationFailed(FirebaseException e) {

                        }
                    };
        });

        findViewById(R.id.sendsignin).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                signinAuth();
            }

            private void signinAuth() {
                String entercode=otp.getText().toString();
                PhoneAuthCredential credential=PhoneAuthProvider.getCredential(vid,entercode);
                signincredential(credential);
            }
            private void signincredential(PhoneAuthCredential credential) {
                auth.signInWithCredential(credential).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {

                        if (task.isSuccessful())
                        {
                            Toast.makeText(MainActivity.this, "sucess", Toast.LENGTH_SHORT).show();
                        }
                        else
                        {

                            if (task.getException() instanceof FirebaseAuthInvalidCredentialsException)
                            {
                                Toast.makeText(MainActivity.this, "wrong otp", Toast.LENGTH_SHORT).show();

                            }
                        }
                    }

                });

            }
        });
    }
}


```

# Download Code 

https://github.com/AP-Skill-Development-Corporation/AdvancedAndroid/tree/master/GopalOtpAuth

# ------------------------------------------------------------------------------

# Firebase Google Sign-In Authentication

Firebase provides different types of Authentication methods. In our previous section, we learned how authentication is done using Firebase UI and Firebase SDK. In this section, we will learn another method, i.e., Google Sign-in Authentication. It is pretty easy to do.

Starting steps are the same as we have done with other authentication methods, which are as follows:

* Creating an Android project.
* Creating a Firebase project.
* Adding Firebase to the Android project or application, either manually or Firebase Assistance.
* Adding the required libraries and JSON files.

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


# Download Code:

https://github.com/AP-Skill-Development-Corporation/AdvancedAndroid/tree/master/GoogleSignInAuthentication

# ------------------------------------------------------------------------------

# Firebase: Facebook Sign-In Authentication

we will talk about the most trending authentication method of Firebase, i.e., Facebook. Facebook sign-in authentication is quite typical to implement.
The users can authenticate with Firebase using their Facebook accounts by integrating Facebook logging into our application.

So let's see the steps to implement Facebook sign-in authentication one by one.

# Step 1:
In the first step, we will create an Android and Firebase project, and then we will add our Firebase project with our application. Also, add SHA-1 and SHA-256 keys in the Firebase console. After that, add all the required dependencies, i.e., firebase-core, firebase-auth, and plugin in 'app.build.gradle' file and classpath in 'build.gradle' file.

We will also add the Facebook login dependency in the 'app.build.gradle' file'.

![f1](https://user-images.githubusercontent.com/51777024/85914350-8bc91500-b85a-11ea-9364-0578c1588912.png)

# Step 2:

In the next step, we have to create an application in the 'Facebook for developer' website. For creating a request, we should have a Facebook account. Login with the Facebook account. Then, go to the Facebook developer site with the help of the following link:

https://developers.facebook.com/

![f2](https://user-images.githubusercontent.com/51777024/85914353-91265f80-b85a-11ea-947e-66c0ebb56ce1.png)

Once our developer account is logged in, we will click on Docs to move on to the document page.

![f3](https://user-images.githubusercontent.com/51777024/85914356-95eb1380-b85a-11ea-9791-b3bb8b2ac0d5.png)

# Step 3:

In the document page, we will scroll down and click on the Facebook login. And from the Facebook login page, we will select Android to move an android page from there, we will select an app or create a new app.

![f4](https://user-images.githubusercontent.com/51777024/85914360-9b485e00-b85a-11ea-8f36-b0f9cf56e781.png)

![f5](https://user-images.githubusercontent.com/51777024/85914364-9f747b80-b85a-11ea-9e46-3ef82cb6ddc9.png)

If we are not a developer, then we have to register as a developer by clicking on Register.

![f6](https://user-images.githubusercontent.com/51777024/85914366-a56a5c80-b85a-11ea-9ac1-8a3fc13b03f5.png)

Click on next to register as a Facebook developer.

![f7](https://user-images.githubusercontent.com/51777024/85914368-a8fde380-b85a-11ea-8bc9-6e40bf48e411.png)

After clicking on the next, a new screen will be visible from where select the developer option.

![f8](https://user-images.githubusercontent.com/51777024/85914370-ac916a80-b85a-11ea-80cb-41b11c876aa4.png)

After selecting developer, the welcome page will be opened.

![f9](https://user-images.githubusercontent.com/51777024/85914374-b1561e80-b85a-11ea-9892-89e4d13e2a70.png)

From the welcome page, select Create First App and give it a name for display and contact email and click on Create App ID.

![f10](https://user-images.githubusercontent.com/51777024/85914377-b4510f00-b85a-11ea-8448-f0e88a05bc9e.png)

Perform a security check.

![f11](https://user-images.githubusercontent.com/51777024/85914381-b7e49600-b85a-11ea-87e1-34b77d80e496.png)

![f12](https://user-images.githubusercontent.com/51777024/85914384-badf8680-b85a-11ea-94e2-339dfa4b31a6.png)

Now, go to Home->Doc->facebook login->android and select the app which we have created before and copied the App ID.

![f13](https://user-images.githubusercontent.com/51777024/85914386-bf0ba400-b85a-11ea-9247-0acd7e2cbaac.png)


# Step 4:

In the next step, we will move to the 'string.xml' file of Android Studio and create two strings, i.e., facebook_app_id and fb_login_protocol_scheme. For facebook_app_id, we will paste the app id, which we have copied before, and for fb_login_protocol_scheme, we will add prefix FB in our app_id and use it as a protocol string.

![f14](https://user-images.githubusercontent.com/51777024/85914387-c29f2b00-b85a-11ea-9219-32ab5fcbeae3.png)

# Step 5:

We also need to add permission for the Internet to our Android Manifest file.

![f15](https://user-images.githubusercontent.com/51777024/85914388-c59a1b80-b85a-11ea-8d5f-dbd6ca6b48e4.png)

# Step 6:

In the next step, we will add the Metadata. For this, we will go to the Facebook developer site and copy the code of step 5.

![f16](https://user-images.githubusercontent.com/51777024/85914389-c92da280-b85a-11ea-8ffd-c1b7036c3441.png)

After copying the code, we will paste it in Manifest files after the MainActivity code.

![f17](https://user-images.githubusercontent.com/51777024/85914392-cc289300-b85a-11ea-8314-d988d7d391ea.png)

# Step 7:

Now, we will associate our package name and default class with our app. So we will add the package name and default activity class name in the developer site.

![f18](https://user-images.githubusercontent.com/51777024/85914395-ce8aed00-b85a-11ea-8d20-3f1fbabc2d83.png)

# Step 8:

In the next step, we will add the Development Key Hashes for our app. For this, we need openssl open library. If we don't have this library, then we first have to download the openssl library. And after that we will execute the following command in the command prompt:

![f19](https://user-images.githubusercontent.com/51777024/85914398-d0ed4700-b85a-11ea-985a-a79f9aaac4d6.png)

We will copy this key and paste it in the developer site's Key Hashes

![f20](https://user-images.githubusercontent.com/51777024/85914400-d3e83780-b85a-11ea-8660-c5952970713a.png)

# Step 9:

In the next step, we have to enable single sign-on for our app in facebook developer sites.

![f21](https://user-images.githubusercontent.com/51777024/85914404-d77bbe80-b85a-11ea-82a0-f83afaf2cfbc.png)

# Step 10:

In the next step, we will go to the basic setting of our app in the facebook developer site. And from here, we have to copy the App Secret that will be used in Firebase console.

![f22](https://user-images.githubusercontent.com/51777024/85914405-d9de1880-b85a-11ea-8c7f-c338266f2d52.png)

# Step 11:

The App Secret, which we have copied from the Facebook developer site, will be pasted in the firebase console. When we enable the Facebook sign-in method, it will ask for the App ID and App Secret and provide OAuth redirect URL, which will be added to our app on the Facebook developer site.

![f23](https://user-images.githubusercontent.com/51777024/85914406-dcd90900-b85a-11ea-990b-c0914e432c93.png)

Now, we will go to the Facebook setting page. Here, we will add the OAuth redirect URL to Facebook login settings.

![f24](https://user-images.githubusercontent.com/51777024/85914408-df3b6300-b85a-11ea-9624-30357ce75f42.png)

# Step 12:

In the next step, we will create a Facebook login button from the SDK. It is a UI element that wraps functionality available in the login manager.

![f25](https://user-images.githubusercontent.com/51777024/85914409-e2365380-b85a-11ea-8798-03b9eb915fec.png)

# Step 13:

In the next step, we will modify our MainActivity.java file to perform the authentication using Facebook in the following way:

```
public class MainActivity extends AppCompatActivity {  
  
    private static final String TAG = "FacebookLogin";  
    private static final int RC_SIGN_IN = 12345;  
  
    private CallbackManager mCallbackManager;  
  
    private FirebaseAuth mAuth;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
  
        // Initialize Firebase Auth  
        mAuth = FirebaseAuth.getInstance();  
  
        // Initialize Facebook Login button  
        mCallbackManager = CallbackManager.Factory.create();  
  
        LoginButton loginButton = findViewById(R.id.login_button);  
  
        loginButton.setReadPermissions("email", "public_profile");  
        loginButton.registerCallback(mCallbackManager, new FacebookCallback<LoginResult>() {  
            @Override  
            public void onSuccess(LoginResult loginResult) {  
                Log.d(TAG, "facebook:onSuccess:" + loginResult);  
                handleFacebookAccessToken(loginResult.getAccessToken());  
            }  
  
            @Override  
            public void onCancel() {  
                Log.d(TAG, "facebook:onCancel");  
            }  
  
            @Override  
            public void onError(FacebookException error) {  
  
            }  
  
        });  
    }  
  
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
    @Override  
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {  
        super.onActivityResult(requestCode, resultCode, data);  
  
        // The activity result pass back to the Facebook SDK  
        mCallbackManager.onActivityResult(requestCode, resultCode, data);  
    }  
  
    private void handleFacebookAccessToken(AccessToken token) {  
        Log.d(TAG, "handleFacebookAccessToken:" + token);  
  
        AuthCredential credential = FacebookAuthProvider.getCredential(token.getToken());  
  
        mAuth.signInWithCredential(credential)  
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {  
                    @Override  
                    public void onComplete(@NonNull Task<AuthResult> task) {  
                        if (task.isSuccessful()) {  
                            // Sign in success, UI will update with the signed-in user's information  
                            Log.d(TAG, "signInWithCredential:success");  
                            FirebaseUser user = mAuth.getCurrentUser();  
                            Toast.makeText(MainActivity.this, "Authentication Succeeded.", Toast.LENGTH_SHORT).show();  
                        } else {  
                            // If sign-in fails, a message will display to the user.  
                            Log.w(TAG, "signInWithCredential:failure", task.getException());  
                            Toast.makeText(MainActivity.this, "Authentication failed.", Toast.LENGTH_SHORT).show();  
                        }  
                    }  
                });  
    }  
}  
```
# Output:

![f26](https://user-images.githubusercontent.com/51777024/85914411-e5c9da80-b85a-11ea-9c8b-8bc80de000ac.png)

![f28](https://user-images.githubusercontent.com/51777024/85914810-71456a80-b85f-11ea-9bf2-17b9b0eeb0e0.png)

![f27](https://user-images.githubusercontent.com/51777024/85914415-f712e700-b85a-11ea-956b-91133e7edf64.png)

# UploadimagesFirebaseStorage
## Creating a new Project
* As always the first step is creating a new Android Studio Project.
* So just create a new Android Studio project using an Empty Activity. 
* I created a project named FirebaseStorage.
* Once your project is loaded, you can add Firebase storage to it.
## Adding FirebaseStorage
* With new Android 2.2 it is really easy to integrate firebase. (If you haven’t updated your studio, you should update your Android Studio).
* To add Firebase Storage, click on Tools -> Firebase

![a1](https://user-images.githubusercontent.com/51777024/85916762-80351880-b871-11ea-95cd-2174c926fb4f.png)

* An assistant window would open in left with all the firebase features. We have to select Firebase Storage from the list.

![a2](https://user-images.githubusercontent.com/51777024/85916764-83c89f80-b871-11ea-87db-fb8996243c40.png)

* Now you will see a link saying Upload and Download a File with Firebase Storage click on it.

![a3](https://user-images.githubusercontent.com/51777024/85916765-875c2680-b871-11ea-9d93-62ecb04d6f31.png)

Now you will see again the same screen we seen in the last Firebase Cloud Messaging Tutorial. You have to do the same things.

# Connect your app to firebase

Click  on Connect to Firebase. You will see a dialog asking to create a new firebase app or choose an existing one.

![a4](https://user-images.githubusercontent.com/51777024/85916767-8a571700-b871-11ea-8477-aea6fac04ca7.png)

# Adding Firebase Storage

Now Click on the second button Add Firebase Storage to Your App. 

![a5](https://user-images.githubusercontent.com/51777024/85916771-8d520780-b871-11ea-8c0c-6af9b4683c09.png)

* Then click on accept changes and firebase storage is added.

![a6](https://user-images.githubusercontent.com/51777024/85916775-904cf800-b871-11ea-9273-dd7fa360ee24.png)

# Getting a File to Upload
* If we need to upload a file, then the first step is getting that file.
* For this we will create a File Chooser.
# Creating File Chooser
* First we will create layout for our file chooser.
# Creating Layout
* Come inside activity_main.xml and write the following code.
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="net.simplifiedcoding.firebasestorage.MainActivity">
 
    <LinearLayout
        android:id="@+id/linearLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
 
        <Button
            android:id="@+id/buttonChoose"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Choose" />
 
        <Button
            android:id="@+id/buttonUpload"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Upload" />
 
    </LinearLayout>
 
    <ImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@id/linearLayout" />
 
</RelativeLayout>

```
* The above xml code will generate the following layout.

![a7](https://user-images.githubusercontent.com/51777024/85916777-9347e880-b871-11ea-837d-dfa780310a0c.png)

* Now we will code the functionality to the choose button. When we tap the choose button Image Chooser should open. So lets do it.

# Coding File Chooser
Come inside MainActivity.java, and write the following code.

```
package net.simplifiedcoding.firebasestorage;
 
import android.content.Intent;
import android.graphics.Bitmap;
import android.net.Uri;
import android.provider.MediaStore;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
 
import java.io.IOException;
 
public class MainActivity extends AppCompatActivity implements View.OnClickListener /*  implementing click listener */ {
    //a constant to track the file chooser intent
    private static final int PICK_IMAGE_REQUEST = 234;
 
    //Buttons
    private Button buttonChoose;
    private Button buttonUpload;
 
    //ImageView
    private ImageView imageView;
 
    //a Uri object to store file path
    private Uri filePath;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        //getting views from layout
        buttonChoose = (Button) findViewById(R.id.buttonChoose);
        buttonUpload = (Button) findViewById(R.id.buttonUpload);
 
        imageView = (ImageView) findViewById(R.id.imageView);
 
        //attaching listener
        buttonChoose.setOnClickListener(this);
        buttonUpload.setOnClickListener(this);
    }
 
    //method to show file chooser
    private void showFileChooser() {
        Intent intent = new Intent();
        intent.setType("image/*");
        intent.setAction(Intent.ACTION_GET_CONTENT);
        startActivityForResult(Intent.createChooser(intent, "Select Picture"), PICK_IMAGE_REQUEST);
    }
 
    //handling the image chooser activity result
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == PICK_IMAGE_REQUEST && resultCode == RESULT_OK && data != null && data.getData() != null) {
            filePath = data.getData();
            try {
                Bitmap bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), filePath);
                imageView.setImageBitmap(bitmap);
 
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
 
    @Override
    public void onClick(View view) {
        //if the clicked button is choose
        if (view == buttonChoose) {
            showFileChooser();
        }
        //if the clicked button is upload
        else if (view == buttonUpload) {
 
        }
    }
}
```
# Testing File Chooser

Now you can run your application to check whether the file chooser is working or not.

![a8](https://user-images.githubusercontent.com/51777024/85916781-980c9c80-b871-11ea-8789-e6b88f8e1af9.png)

As you can see it is working absolutely fine. So now we can move ahead to learn the main topic of this Firebase Storage Tutorial, which is uploading a file.

# Uploading Selected Image
* We have the chosen image. Now when the user will tap the upload button the file should be uploaded to Firebase Storage.

# Coding Upload Method
* So inside MainActivity class create a method named uploadFile() and write the following code for it.
```
//this method will upload the file
    private void uploadFile() {
        //if there is a file to upload
        if (filePath != null) {
            //displaying a progress dialog while upload is going on
            final ProgressDialog progressDialog = new ProgressDialog(this);
            progressDialog.setTitle("Uploading");
            progressDialog.show();
 
            StorageReference riversRef = storageReference.child("images/pic.jpg");
            riversRef.putFile(filePath)
                    .addOnSuccessListener(new OnSuccessListener<UploadTask.TaskSnapshot>() {
                        @Override
                        public void onSuccess(UploadTask.TaskSnapshot taskSnapshot) {
                            //if the upload is successfull
                            //hiding the progress dialog
                            progressDialog.dismiss();
 
                            //and displaying a success toast
                            Toast.makeText(getApplicationContext(), "File Uploaded ", Toast.LENGTH_LONG).show();
                        }
                    })
                    .addOnFailureListener(new OnFailureListener() {
                        @Override
                        public void onFailure(@NonNull Exception exception) {
                            //if the upload is not successfull
                            //hiding the progress dialog
                            progressDialog.dismiss();
 
                            //and displaying error message
                            Toast.makeText(getApplicationContext(), exception.getMessage(), Toast.LENGTH_LONG).show();
                        }
                    })
                    .addOnProgressListener(new OnProgressListener<UploadTask.TaskSnapshot>() {
                        @Override
                        public void onProgress(UploadTask.TaskSnapshot taskSnapshot) {
                            //calculating progress percentage
                            double progress = (100.0 * taskSnapshot.getBytesTransferred()) / taskSnapshot.getTotalByteCount();
 
                            //displaying percentage in progress dialog
                            progressDialog.setMessage("Uploaded " + ((int) progress) + "%...");
                        }
                    });
        }
        //if there is not any file
        else {
            //you can display an error toast
        }
    }

```

* Now call this method when the button upload is clicked.

```
@Override
    public void onClick(View view) {
        //if the clicked button is choose
        if (view == buttonChoose) {
            showFileChooser();
        }
        //if the clicked button is upload
        else if (view == buttonUpload) {
            uploadFile();
        }
    }
```
* If you will try running the application it will not work, because of the default Storage Rules.

# Changing the Default Rules
* Because the default rules says, only authenticated users will be able to read or write the Firebase Storage. But we haven’t done any authentication in our application.
* So for now we are changing the Firebase Storage Rules.
* So go to Firebase Console and open your Firebase Project. Then from the left menu select Firebase Storage and go to the Rules tab.

![a9](https://user-images.githubusercontent.com/51777024/85916784-9c38ba00-b871-11ea-96bc-49e3d415bbae.png)

* You can see I have changed the rule. So you have to change the rule as shown above. Before it was if auth != null but I changed it to if true so the if will always evaluate true.
* But you should use this only for development purpose. As for production you cannot use this way that anyone can access storage. 

# Testing the Upload
Now just run your application.

![a10](https://user-images.githubusercontent.com/51777024/85916787-9fcc4100-b871-11ea-88b4-5d68ddaf4fe6.png)

* You can also check the firebase storage to check whether the file is uploaded or not.

![a11](https://user-images.githubusercontent.com/51777024/85916790-a3f85e80-b871-11ea-919a-831dbd39b10a.png)

# Retrieving Files from Firebase Storage
* Now we will create a new activity where we display all the uploaded images with labels.
* So create a new activity named ShowImagesActivity and inside the layout file of this activity we will create a RecyclerView.
# Adding RecyclerView and CardView
* First we need to add dependencies for RecyclerView and CardView.
* Go to File -> Project Structure and go to dependencies tab. Here click on plus icon and select Library dependency.



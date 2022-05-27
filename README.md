# issue 3755
### Summary
Reauthentication generates a user within the Firebase console even if the process fails.
### Prerequisite
- Add SHA1
- Add google-services.json
- Create a [OAuth 2.0 client token](https://console.cloud.google.com/apis/credentials) of type `Web application`
    - Add the generated Client Id in code line 56 in `GoogleSignInFragment.kt`
- Enable Google in Sign-in method in Firebase Auth
    - When enabling, add the Client Id and Client Secret generated from the previous step to the Web SDK configuration of the Google Sign In.
- **Important**: wait for 5 mins up to an hour for the changes to apply before signing/logging in.
### Steps to reproduce
- Sign in using a gmail account e.g. `test1@gmail.com`
- Uncomment line 68 - 70, this will run reauthentication
- Close and reopen the app, a redirect of reauth will appear. Login with another account e.g. `test2@gmail.com`.
- `test2@gmail.com` will be added in the Firebase Auth list of logins, even though the logs clearly states that the reauth failed.

P.S. If there's an error regarding redirect_uri mismatch. Add the redirect_uri indicated from the error to the OAuth 2.0 > Authorized redirect URIs. Then wait for 5 mins up to an hour again.

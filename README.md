# B2C_IEF Terms of Service Example Policies

This set of policies I created is based off of the official azure sample policies starter pack repo (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack), this repo contains functionality for LocalAccount Sign-up and sign-in, sign-in only (for direct navigation), profile edit, password reset, all checked with TOS (Terms of Service) on the last steps of the UserJourneys. I did start integrating the google sign in as well, but it is disconnected in the current UserJourneys (shouldn't throw an error if you ignore it). 
To use on your tenant: 
1) Search for yourb2ctenant.onmicrosoft.com and replace with your B2C tenant domain address (To create a B2C tenant please follow the official docs: https://docs.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-tenant). 
2) Replace the Ids with your tenants Ids client_id & resource_id
3) Upload policies in order -> TrustFrameworkBase -> TrustFrameworkExtensions -> SignUpSignIn_TOS/SignUp (SignUp if you want direct navigation) -> TOS/ProfileEdit/PasswordReset

# Password Reset

Reset Local Account password (user in your b2c tenant) - sends authentication code to the users email, confirms code, and then resets the the B2C tenant user's password based on new desired password matching the correct Regex.
Snippet from new password Claim in Base policy (the new Password variable): 

<Restriction>
    <Pattern RegularExpression="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" HelpText="8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." />
</Restriction>

# Profile Edit

Profile edit works specifically for changing the username of the B2C local account user and then checks TOS.

# SUSI (Sign-up Sign-in)

Sign in page containing login controls with a link to the sign up page and password reset (password reset link created in custom UI). Sign in checks for TOS, if not up-to-date then they will be reprompted to accept the most recent TOS. Sign Up restricts access to 

# Sign-up Only

For direct navigation to the sign-up page. This is useful in cases where you need to send an invite link or you want to drop off the user directly on the sign-up page.

# TOS (Terms of Service)

Terms of Service compares extension_termsOfUseConsentDateTime variable to the set datetime a
![Logo of the project](https://raw.githubusercontent.com/csharpener22/B2C-IEF-Custom-Policies-LocalwithTOS/main/images/claims_exchange_flow.png)

# [B2C IEF] (Email) LocalAccount Terms of Service Policies
> This set of policies I created is based off of the official azure sample policies starter pack repo (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

This repo contains functionality for LocalAccount Sign-up and sign-in, sign-in only (for direct navigation), profile edit, password reset, all checked with TOS (Terms of Service) on the last steps of the UserJourneys. I did start integrating the google sign in as well, but it is disconnected in the current UserJourneys (shouldn't throw an error if you ignore it). 

# Getting Started

To use on your tenant:
1) Search for yourb2ctenant.onmicrosoft.com and replace with your B2C tenant domain address 
> (To create a B2C tenant please follow the official docs: https://docs.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-tenant).

2) Replace the Ids with your tenants Ids client_id & resource_id
> You will find these Ids under the Identity Experience Framework Section of your B2C Tenant.

3) Upload policies in order -> TrustFrameworkBase -> TrustFrameworkExtensions -> SignUpSignIn_TOS/SignUp (SignUp if you want direct navigation) -> TOS/ProfileEdit/PasswordReset
> Policies need to be uploaded in the order of their inheritance starting with Base, then Extensions, and finally all the other Userflows.

# Password Reset

Reset Local Account password (user in your b2c tenant) - sends authentication code to the users email, confirms code, and then resets the the B2C tenant user's password based on new desired password matching the correct Regex.

# Profile Edit

Profile edit works specifically for changing the username of the B2C local account user and then checks TOS.

# SUSI (Sign-up Sign-in)

Sign in page containing login controls with a link to the sign up page and password reset (password reset link created in custom UI). Sign in checks for TOS, if not up-to-date then they will be reprompted to accept the most recent TOS.

# Sign-up Only

For direct navigation to the sign-up page. This is useful in cases where you need to send an invite link or you want to drop off the user directly on the sign-up page.

# TOS (Terms of Service)

Terms of Service compares extension_termsOfUseConsentDateTime variable to the currentTime variable and termsOfUseTextUpdateDateTime. Replace value in termsOfUseTextUpdateDateTime for an updated trigger to new TOS.
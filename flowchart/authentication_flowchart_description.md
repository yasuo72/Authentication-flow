# Authentication Module Flowchart for B2B SaaS Product

## Flowchart Components
- **Oval**: Start/End of a process
- **Parallelogram**: User input (only 1 outgoing arrow)
- **Diamond**: Decision point (Yes/No only – max 2 arrows)
- **Rectangle**: Backend/system process (API call, validation, etc.)

## Main Authentication Flows

### 1. Email/Password Login
- **Start** (Oval) → User arrives at login page
- **User Input** (Parallelogram) → Enter email and password
- **System Process** (Rectangle) → Validate input format
- **Decision** (Diamond) → Input format valid?
  - No → Return to User Input with error message
  - Yes → Continue
- **System Process** (Rectangle) → Check if email exists in database
- **Decision** (Diamond) → Email exists?
  - No → Show error message "Email not found"
  - Yes → Continue
- **System Process** (Rectangle) → Verify password hash
- **Decision** (Diamond) → Password correct?
  - No → Show error message "Incorrect password"
  - Yes → Continue
- **Decision** (Diamond) → MFA enabled for account?
  - No → Proceed to successful login
  - Yes → Proceed to MFA flow
- **End** (Oval) → User logged in successfully

### 2. Social Sign-In (Google, LinkedIn)
- **Start** (Oval) → User arrives at login page
- **User Input** (Parallelogram) → Click on social sign-in option
- **System Process** (Rectangle) → Redirect to OAuth provider
- **User Input** (Parallelogram) → Authenticate with provider
- **System Process** (Rectangle) → Receive OAuth callback
- **Decision** (Diamond) → Authentication successful?
  - No → Show error message
  - Yes → Continue
- **System Process** (Rectangle) → Retrieve user profile from provider
- **Decision** (Diamond) → Email exists in our system?
  - No → Proceed to account creation flow
  - Yes → Continue
- **Decision** (Diamond) → MFA enabled?
  - No → Proceed to successful login
  - Yes → Proceed to MFA flow
- **End** (Oval) → User logged in successfully

### 3. Single Sign-On (SSO)
- **Start** (Oval) → User arrives at login page
- **User Input** (Parallelogram) → Enter company email or domain
- **System Process** (Rectangle) → Check if domain has SSO configured
- **Decision** (Diamond) → SSO configured?
  - No → Show error message
  - Yes → Continue
- **System Process** (Rectangle) → Redirect to Identity Provider (IdP)
- **User Input** (Parallelogram) → Authenticate with IdP
- **System Process** (Rectangle) → Process SAML/OIDC response
- **Decision** (Diamond) → Authentication successful?
  - No → Show error message
  - Yes → Continue
- **Decision** (Diamond) → User exists in our system?
  - No → Create user account (JIT provisioning)
  - Yes → Continue
- **Decision** (Diamond) → MFA required by policy?
  - No → Proceed to successful login
  - Yes → Proceed to MFA flow
- **End** (Oval) → User logged in successfully

### 4. Multi-Factor Authentication (MFA)
- **Start** (Oval) → User successfully passed primary authentication
- **System Process** (Rectangle) → Generate MFA challenge
- **Decision** (Diamond) → "Remember this device" enabled and device recognized?
  - Yes → Skip MFA and proceed to successful login
  - No → Continue with MFA
- **User Input** (Parallelogram) → Select MFA method (SMS, Email, Authenticator App)
- **System Process** (Rectangle) → Send/generate verification code
- **User Input** (Parallelogram) → Enter verification code
- **System Process** (Rectangle) → Validate code
- **Decision** (Diamond) → Code valid?
  - No → Show error message, allow retry (limited attempts)
  - Yes → Continue
- **User Input** (Parallelogram) → Optional: "Remember this device" checkbox
- **System Process** (Rectangle) → Store device token if requested
- **End** (Oval) → MFA successful, proceed to login

### 5. Account Creation
- **Start** (Oval) → New user registration
- **User Input** (Parallelogram) → Enter email, password, and profile information
- **System Process** (Rectangle) → Validate input format
- **Decision** (Diamond) → Input valid?
  - No → Show validation errors
  - Yes → Continue
- **System Process** (Rectangle) → Check if email already exists
- **Decision** (Diamond) → Email exists?
  - Yes → Show error message
  - No → Continue
- **Decision** (Diamond) → Captcha required?
  - Yes → Show captcha challenge
  - No → Skip captcha
- **User Input** (Parallelogram) → Complete captcha (if required)
- **System Process** (Rectangle) → Verify captcha
- **System Process** (Rectangle) → Create user account
- **System Process** (Rectangle) → Generate email verification token
- **System Process** (Rectangle) → Send verification email
- **End** (Oval) → Account created, verification email sent

### 6. Account/Password Recovery
- **Start** (Oval) → User clicks "Forgot Password"
- **User Input** (Parallelogram) → Enter email address
- **System Process** (Rectangle) → Check if email exists
- **Decision** (Diamond) → Email exists?
  - No → Show same success message (security by obscurity)
  - Yes → Continue
- **System Process** (Rectangle) → Generate password reset token
- **System Process** (Rectangle) → Send password reset email
- **User Input** (Parallelogram) → Click reset link in email
- **System Process** (Rectangle) → Validate reset token
- **Decision** (Diamond) → Token valid and not expired?
  - No → Show error message
  - Yes → Continue
- **User Input** (Parallelogram) → Enter new password (and confirm)
- **System Process** (Rectangle) → Validate password strength
- **Decision** (Diamond) → Password meets requirements?
  - No → Show error message
  - Yes → Continue
- **System Process** (Rectangle) → Update password in database
- **System Process** (Rectangle) → Invalidate all active sessions
- **System Process** (Rectangle) → Send password change notification
- **End** (Oval) → Password reset successful

## Optional Steps
- **Captcha**: Integrated into registration and password recovery flows
- **Remember Device**: Integrated into MFA flow
- **Session Management**: Timeout settings, concurrent sessions
- **Account Lockout**: After multiple failed login attempts

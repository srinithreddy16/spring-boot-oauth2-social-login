# Spring OAuth2 Application

A Spring Boot application demonstrating OAuth2 authentication with Google and GitHub providers. This application allows users to authenticate using their Google or GitHub accounts.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [OAuth2 Configuration](#oauth2-configuration)
  - [Google OAuth2 Setup](#google-oauth2-setup)
  - [GitHub OAuth2 Setup](#github-oauth2-setup)
- [Environment Variables](#environment-variables)
- [Running the Application](#running-the-application)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)

## Prerequisites

Before you begin, ensure you have the following installed:

- **Java 21** or higher
- **Maven 3.6+** (or use the included Maven Wrapper)
- **Google Account** (for Google OAuth2 setup)
- **GitHub Account** (for GitHub OAuth2 setup)

## Getting Started

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd SpringOauth2
   ```

2. Configure OAuth2 credentials (see sections below)

3. Set up environment variables (see [Environment Variables](#environment-variables) section)
   - A `.env` file template is provided in the project root
   - Replace the dummy values with your actual OAuth2 credentials

4. Run the application

## OAuth2 Configuration

### Google OAuth2 Setup

Follow these steps to obtain your Google Client ID and Client Secret:

#### Step 1: Access Google Cloud Console

1. Navigate to the [Google Cloud Console](https://console.cloud.google.com/)
2. Sign in with your Google account

#### Step 2: Create a New Project

1. Click on the project dropdown at the top of the page
2. Click **"New Project"**
3. Enter a project name (e.g., "Spring OAuth2 App")
4. Click **"Create"**
5. Wait for the project to be created and select it from the dropdown

#### Step 3: Enable Google+ API

1. In the left sidebar, navigate to **"APIs & Services"** > **"Library"**
2. Search for **"Google+ API"** or **"Google Identity"**
3. Click on **"Google+ API"** or **"Google Identity Services API"**
4. Click **"Enable"**

#### Step 4: Configure OAuth Consent Screen

1. Navigate to **"APIs & Services"** > **"OAuth consent screen"**
2. Select **"External"** user type (unless you have a Google Workspace account)
3. Click **"Create"**
4. Fill in the required information:
   - **App name**: Enter your application name
   - **User support email**: Select your email
   - **Developer contact information**: Enter your email
5. Click **"Save and Continue"**
6. On the **Scopes** page, click **"Save and Continue"** (you can add scopes later if needed)
7. On the **Test users** page, add test users if needed, then click **"Save and Continue"**
8. Review and click **"Back to Dashboard"**

#### Step 5: Create OAuth2 Credentials

1. Navigate to **"APIs & Services"** > **"Credentials"**
2. Click **"+ CREATE CREDENTIALS"** at the top
3. Select **"OAuth client ID"**
4. If prompted, select **"Web application"** as the application type
5. Configure the OAuth client:
   - **Name**: Enter a descriptive name (e.g., "Spring OAuth2 Client")
   - **Authorized JavaScript origins**: 
     - For local development: `http://localhost:8080`
     - Add your production URL when deploying
   - **Authorized redirect URIs**:
     - For local development: `http://localhost:8080/login/oauth2/code/google`
     - Add your production callback URL when deploying
6. Click **"Create"**
7. A popup will display your **Client ID** and **Client Secret**
   - **Important**: Copy these values immediately as the Client Secret will not be shown again
   - If you lose the Client Secret, you'll need to create a new OAuth client

#### Step 6: Save Your Credentials

- **Client ID**: Copy this value (it looks like: `123456789-abcdefghijklmnop.apps.googleusercontent.com`)
- **Client Secret**: Copy this value (it looks like: `GOCSPX-abcdefghijklmnopqrstuvwxyz`)

---

### GitHub OAuth2 Setup

Follow these steps to obtain your GitHub Client ID and Client Secret:

#### Step 1: Access GitHub Developer Settings

1. Log in to your [GitHub account](https://github.com/)
2. Click on your profile picture in the top right corner
3. Select **"Settings"** from the dropdown menu
4. In the left sidebar, scroll down and click **"Developer settings"**

#### Step 2: Create a New OAuth App

1. In the Developer settings, click **"OAuth Apps"** in the left sidebar
2. Click **"New OAuth App"** button (or **"Register a new application"**)

#### Step 3: Configure OAuth App

Fill in the application details:

- **Application name**: Enter a descriptive name (e.g., "Spring OAuth2 Application")
- **Homepage URL**: 
  - For local development: `http://localhost:8080`
  - Use your production URL when deploying
- **Application description**: (Optional) Describe your application
- **Authorization callback URL**: 
  - For local development: `http://localhost:8080/login/oauth2/code/github`
  - Use your production callback URL when deploying

#### Step 4: Register the Application

1. Click **"Register application"**
2. You'll be redirected to the application details page

#### Step 5: Generate Client Secret

1. On the application details page, you'll see your **Client ID** (it's visible immediately)
2. Click **"Generate a new client secret"** button
3. A new **Client Secret** will be generated
   - **Important**: Copy this value immediately as it will only be shown once
   - If you lose the Client Secret, you'll need to generate a new one

#### Step 6: Save Your Credentials

- **Client ID**: Copy this value (it looks like: `Iv1.8a61f9b3a7aba766`)
- **Client Secret**: Copy this value (it looks like: `a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6`)

---

## Environment Variables

This application uses environment variables to securely store OAuth2 credentials. You have several options to set them:

### Option 1: Using .env File (Recommended for Local Development)

A `.env` file template is provided in the project root with dummy values. To use it:

1. Open the `.env` file in the project root
2. Replace the dummy values with your actual OAuth2 credentials:
   ```env
   GOOGLE_CLIENT_ID=your-actual-google-client-id
   GOOGLE_CLIENT_SECRET=your-actual-google-client-secret
   GITHUB_CLIENT_ID=your-actual-github-client-id
   GITHUB_CLIENT_SECRET=your-actual-github-client-secret
   ```

**Note:** Spring Boot doesn't automatically load `.env` files. You have two options:

**Option A: Use a dotenv library (Recommended)**
- Add `io.github.cdimascio:dotenv-java` dependency to your `pom.xml`
- The library will automatically load the `.env` file

**Option B: Manually load environment variables**
- Use the `.env` file as a reference
- Set the environment variables in your system or IDE (see Option 2 below)

**⚠️ Important:** The `.env` file is already in `.gitignore` to prevent committing credentials to version control.

### Option 2: System Environment Variables

**Windows (PowerShell):**
```powershell
$env:GOOGLE_CLIENT_ID="your-google-client-id"
$env:GOOGLE_CLIENT_SECRET="your-google-client-secret"
$env:GITHUB_CLIENT_ID="your-github-client-id"
$env:GITHUB_CLIENT_SECRET="your-github-client-secret"
```

**Windows (Command Prompt):**
```cmd
set GOOGLE_CLIENT_ID=your-google-client-id
set GOOGLE_CLIENT_SECRET=your-google-client-secret
set GITHUB_CLIENT_ID=your-github-client-id
set GITHUB_CLIENT_SECRET=your-github-client-secret
```

**Linux/macOS:**
```bash
export GOOGLE_CLIENT_ID="your-google-client-id"
export GOOGLE_CLIENT_SECRET="your-google-client-secret"
export GITHUB_CLIENT_ID="your-github-client-id"
export GITHUB_CLIENT_SECRET="your-github-client-secret"
```

### Option 3: IDE Configuration

If you're using an IDE like IntelliJ IDEA or Eclipse:

1. **IntelliJ IDEA:**
   - Go to **Run** > **Edit Configurations**
   - Select your Spring Boot application configuration
   - Under **Environment variables**, add:
     ```
     GOOGLE_CLIENT_ID=your-google-client-id
     GOOGLE_CLIENT_SECRET=your-google-client-secret
     GITHUB_CLIENT_ID=your-github-client-id
     GITHUB_CLIENT_SECRET=your-github-client-secret
     ```

2. **Eclipse:**
   - Right-click on the project > **Run As** > **Run Configurations**
   - Select your Spring Boot application
   - Go to the **Environment** tab
   - Add the environment variables

### Option 4: Application Properties (Not Recommended for Production)

For local development only, you can directly edit `src/main/resources/application.properties`:

```properties
spring.security.oauth2.client.registration.google.client-id=your-google-client-id
spring.security.oauth2.client.registration.google.client-secret=your-google-client-secret
spring.security.oauth2.client.registration.github.client-id=your-github-client-id
spring.security.oauth2.client.registration.github.client-secret=your-github-client-secret
```

**⚠️ Warning:** Never commit credentials to version control. Always use environment variables or a secure secrets management system in production.

## Running the Application

### Using Maven Wrapper

**Windows:**
```bash
.\mvnw.cmd spring-boot:run
```

**Linux/macOS:**
```bash
./mvnw spring-boot:run
```

### Using Maven (if installed)

```bash
mvn spring-boot:run
```

### Using IDE

1. Open the project in your IDE (IntelliJ IDEA, Eclipse, VS Code)
2. Locate `SpringOauth2Application.java`
3. Run the main method

The application will start on `http://localhost:8080` by default.

## Usage

1. **Start the application** (see [Running the Application](#running-the-application))

2. **Access the application:**
   - Open your browser and navigate to `http://localhost:8080`
   - You'll be redirected to the login page

3. **Authenticate:**
   - Click on either **"Google"** or **"GitHub"** to authenticate
   - You'll be redirected to the respective OAuth provider's login page
   - After successful authentication, you'll be redirected back to the application

4. **Access protected resources:**
   - Once authenticated, you can access the root endpoint (`/`) which returns "Welcome to my application"

## Project Structure

```
SpringOauth2/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/srinith/SpringOauth2/
│   │   │       ├── SpringOauth2Application.java    # Main application class
│   │   │       ├── SecurityConfig.java            # Security configuration
│   │   │       └── HelloController.java           # REST controller
│   │   └── resources/
│   │       ├── application.properties             # Application configuration
│   │       ├── static/                            # Static resources
│   │       └── templates/                         # Thymeleaf templates (if used)
│   └── test/
│       └── java/                                  # Test classes
├── .env                                           # Environment variables (not committed to git)
├── .gitignore                                     # Git ignore rules
├── pom.xml                                        # Maven dependencies
├── mvnw                                           # Maven wrapper (Unix)
├── mvnw.cmd                                       # Maven wrapper (Windows)
└── README.md                                      # This file
```

## Technologies Used

- **Spring Boot 4.0.3** - Application framework
- **Spring Security OAuth2 Client** - OAuth2 authentication
- **Java 21** - Programming language
- **Maven** - Dependency management

## Security Notes

- **Never commit credentials** to version control
- Use environment variables or secure secrets management in production
- Keep your OAuth2 client secrets confidential
- Regularly rotate your OAuth2 credentials
- Use HTTPS in production environments
- Configure appropriate redirect URIs for your environment

## Troubleshooting

### Common Issues

1. **"Invalid client" error:**
   - Verify that your Client ID and Client Secret are correct
   - Ensure environment variables are set properly
   - Check that there are no extra spaces or quotes in the values

2. **"Redirect URI mismatch" error:**
   - Verify that the redirect URI in your OAuth provider matches exactly: `http://localhost:8080/login/oauth2/code/{provider}`
   - For Google: Check the "Authorized redirect URIs" in Google Cloud Console
   - For GitHub: Check the "Authorization callback URL" in GitHub OAuth App settings

3. **Application won't start:**
   - Ensure Java 21 is installed and configured
   - Check that all environment variables are set (verify your `.env` file or system environment variables)
   - Verify Maven dependencies are downloaded
   - If using `.env` file, ensure you've replaced dummy values with actual credentials

4. **OAuth consent screen issues (Google):**
   - Ensure the OAuth consent screen is properly configured
   - If using "External" user type, add test users if the app is in testing mode
   - Verify that the Google+ API or Google Identity Services API is enabled

## License

This project is provided as-is for educational and demonstration purposes.

## Support

For issues or questions, please open an issue in the repository or contact the project maintainer.

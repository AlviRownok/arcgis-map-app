# Interactive ArcGIS Map with User Information and CSV Export

This project is an interactive web application that allows users to draw polygons on an ArcGIS map, calculate the area, fetch places within the polygon using the Overpass API, and save their input along with user information to an AWS S3 bucket as a CSV file. The application also includes a developer section for managing user entries.

## Table of Contents

- [Features](#features)
- [Demo](#demo)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
  - [ArcGIS OAuth Configuration](#arcgis-oauth-configuration)
  - [AWS S3 Configuration](#aws-s3-configuration)
  - [Overpass API](#overpass-api)
- [Running the Application](#running-the-application)
- [Usage Instructions](#usage-instructions)
  - [User Interaction](#user-interaction)
  - [Developer Section](#developer-section)
- [Dependencies](#dependencies)
- [Security Considerations](#security-considerations)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Features

- Interactive ArcGIS map centered on Napoli, Italy.
- User authentication using ArcGIS OAuth 2.0.
- Users can draw polygons on the map using the Sketch widget.
- Calculates the geodesic area of the drawn polygon.
- Fetches place names within the polygon using the Overpass API.
- Stores user information and polygon data.
- Saves data to an AWS S3 bucket as a CSV file.
- Developer section for managing and removing user entries.
- Supports downloading the CSV file locally.

## Demo

[Live Demo](https://alvirownok.github.io/your-repo-name/)

*Note: Replace the above URL with the actual link to your live application on GitHub Pages.*

## Prerequisites

- An [ArcGIS Developer](https://developers.arcgis.com/sign-up/) account.
- An AWS account with S3 and Cognito services configured.
- A GitHub account.
- Basic knowledge of JavaScript, HTML, and CSS.

## Installation

### Hosting the Application on GitHub Pages

Since the application uses OAuth authentication, it must be served over HTTPS. GitHub Pages provides a simple way to host your static website securely over HTTPS.

Follow these steps to host your application on GitHub Pages:

1. **Fork or Clone the Repository**

   - If you haven't already, clone this repository to your local machine:

     ```bash
     git clone https://github.com/your-username/your-repo-name.git
     ```

2. **Push Your Code to GitHub**

   - Navigate to the project directory:

     ```bash
     cd your-repo-name
     ```

   - Initialize a Git repository if you haven't already:

     ```bash
     git init
     ```

   - Add all files to the repository:

     ```bash
     git add .
     ```

   - Commit your changes:

     ```bash
     git commit -m "Initial commit"
     ```

   - Add the remote origin (if not set):

     ```bash
     git remote add origin https://github.com/your-username/your-repo-name.git
     ```

   - Push the code to GitHub:

     ```bash
     git push -u origin main
     ```

     *Note: Replace `main` with your default branch name if different.*

3. **Enable GitHub Pages**

   - Go to your repository on GitHub.
   - Click on **Settings**.
   - In the left sidebar, click on **Pages**.
   - Under **Source**, select the branch you want to use (e.g., `main` or `master`) and the root folder (`/ (root)`).
   - Click **Save**.
   - GitHub Pages will provide you with a URL where your site is hosted, usually `https://your-username.github.io/your-repo-name/`.

4. **Update the ArcGIS OAuth Redirect URI**

   - In your ArcGIS Developer Dashboard, navigate to your application's settings.
   - Update the **Redirect URI** to match your GitHub Pages URL.
     - For example: `https://your-username.github.io/your-repo-name/`

5. **Update the Code with Your GitHub Pages URL**

   - In your HTML file, update the `redirectUri` in the OAuthInfo configuration:

     ```javascript
     const redirectUri = "https://your-username.github.io/your-repo-name/"; // Your application's URL
     ```

6. **Commit and Push Changes**

   - After updating the code, commit and push the changes:

     ```bash
     git add .
     git commit -m "Update redirect URI"
     git push
     ```

7. **Wait for GitHub Pages to Build**

   - It may take a few minutes for GitHub Pages to build and deploy your site.
   - Visit your GitHub Pages URL to access the application.

## Configuration

Before running the application, you need to configure several services:

### ArcGIS OAuth Configuration

1. **Register Your Application**

   - Sign in to your ArcGIS Developer account.
   - Go to the [Dashboard](https://developers.arcgis.com/dashboard) and register a new application.
   - Obtain the **Client ID (App ID)**.

2. **Set the Redirect URI**

   - In your application settings, set the **Redirect URI** to your GitHub Pages URL.
     - Example: `https://your-username.github.io/your-repo-name/`

3. **Update the Code**

   In your HTML file, replace the placeholders with your actual `appId` and `redirectUri`:

   ```javascript
   const appId = "YOUR_APP_ID"; // Replace with your Client ID (App ID)
   const redirectUri = "https://your-username.github.io/your-repo-name/"; // Your GitHub Pages URL
   ```

### AWS S3 Configuration

1. **Set Up an S3 Bucket**

   - Log in to your AWS account.
   - Create a new S3 bucket (e.g., `arcgisapp`).
   - Set appropriate permissions to allow read/write access via AWS SDK.

2. **Configure AWS Cognito Identity Pool**

   - Navigate to AWS Cognito and create a new Identity Pool.
   - Enable access to unauthenticated identities if necessary.
   - Configure the Identity Pool to grant access to your S3 bucket.

3. **Update the Code**

   In your HTML file, update the AWS configuration:

   ```javascript
   AWS.config.update({
       region: 'YOUR_AWS_REGION' // e.g., 'us-east-1'
   });

   AWS.config.credentials = new AWS.CognitoIdentityCredentials({
       IdentityPoolId: 'YOUR_IDENTITY_POOL_ID' // e.g., 'us-east-1:XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX'
   });

   const S3_BUCKET = 'YOUR_S3_BUCKET_NAME'; // e.g., 'arcgisapp'
   const S3_KEY = 'map_features.csv'; // Path to your CSV file
   ```

### Overpass API

The application uses the Overpass API to fetch place names within the drawn polygon. No additional configuration is required, but be mindful of the API's usage limits.

## Running the Application

After completing the configuration:

1. **Access the Application**

   - Open your web browser and navigate to your GitHub Pages URL:

     ```
     https://your-username.github.io/your-repo-name/
     ```

2. **Authentication**

   - The application will prompt you to sign in using your ArcGIS account.
   - Complete the authentication process to access the application.

## Usage Instructions

### User Interaction

1. **User Information**

   - Upon loading the application, fill out the user form with your **Name**, **Surname**, and **Company Name**.
   - Click the **OK** button to proceed.

2. **Drawing Polygons**

   - Use the **Sketch** widget located at the top-right corner of the map to draw a polygon.
   - Click on the map to add vertices and double-click to finish drawing.

3. **Saving Data**

   - After drawing, the area is calculated, and place names within the polygon are fetched.
   - Your polygon is displayed on the map with a label containing your information.
   - Click **Save** to confirm your data has been stored.
   - Use the **Download CSV** button to download the data locally.
   - Click **Done** when you are finished to reset the form.

### Developer Section

1. **Accessing Developer Tools**

   - Click the **Developer Login** button.
   - Enter the developer password (Note: The password should be securely stored and not hardcoded).

2. **Managing User Entries**

   - After successful authentication, you can view a list of user entries.
   - Click **Remove** next to a user to delete their data from the map and the AWS S3 bucket.

## Dependencies

The application relies on the following libraries and APIs:

- [ArcGIS API for JavaScript](https://developers.arcgis.com/javascript/)
- [AWS SDK for JavaScript](https://docs.aws.amazon.com/sdk-for-javascript/)
- [PapaParse](https://www.papaparse.com/) for CSV parsing
- [Overpass API](https://overpass-api.de/) for fetching OSM data

## Security Considerations

- **Sensitive Information**

  - **Never** commit sensitive information like API keys, Client IDs, passwords, or AWS credentials to your repository.
  - Use environment variables or configuration files excluded from version control to store sensitive data.

- **Developer Password**

  - Remove any hardcoded passwords from your code.
  - Implement secure authentication methods for the developer section, such as OAuth or a server-side login.

- **AWS Credentials**

  - Ensure your AWS IAM policies follow the principle of least privilege.
  - Do not expose AWS secret keys in your client-side code.

- **ArcGIS OAuth**

  - Protect your `appId` and ensure the `redirectUri` matches the domain where your app is hosted.
  - Consider using server-side authentication if additional security is required.

## Troubleshooting

- **ArcGIS API Loading Issues**

  - Ensure you have a stable internet connection.
  - Check for any console errors related to loading the ArcGIS API.

- **Authentication Failures**

  - Verify that your `appId` and `redirectUri` are correctly configured.
  - Ensure your application is served over HTTPS, as OAuth 2.0 requires a secure context.

- **AWS S3 Access Issues**

  - Confirm that your AWS credentials are correct.
  - Check the IAM policies to ensure the necessary permissions are granted.
  - Verify that the S3 bucket exists and the `S3_BUCKET` and `S3_KEY` variables are set correctly.

- **Overpass API Errors**

  - Be mindful of the Overpass API rate limits.
  - If you encounter errors, try reducing the frequency of requests or implement caching.

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. Commit your changes:

   ```bash
   git commit -m "Add your message"
   ```

4. Push to the branch:

   ```bash
   git push origin feature/your-feature-name
   ```

5. Open a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

For any questions or inquiries, please contact:

**Alvi Rownok**

- **Phone:** +39 351 204 9968
- **Email:** alvi2241998@gmail.com
- **LinkedIn:** [linkedin.com/in/alvi-rownok](https://www.linkedin.com/in/alvi-rownok/)

---

*Note: Replace placeholders like `YOUR_APP_ID`, `YOUR_AWS_REGION`, `YOUR_IDENTITY_POOL_ID`, and `YOUR_S3_BUCKET_NAME` with your actual configuration values. Also, make sure to secure all sensitive information and follow best practices for handling credentials.*

*Ensure that the `redirectUri` in your code and the redirect URI in your ArcGIS application settings match your GitHub Pages URL.*
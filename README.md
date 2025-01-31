# My Project

## Features
This section describes the features of the project.
## 📌 Table of Contents
- [1. Setting Up Environment Variables](#setting-up-environment-variables)
- [2. Feature Flags](#feature-flags)
- [3. Troubleshooting Common Issues](#troubleshooting-common-issues)

---


## Usage
Learn how to use the project.
Using email notifications with log snippets is a straightforward way to keep developers informed about their Jenkins pipeline runs without requiring them to access Jenkins directly. Here's a detailed guide on how to set this up using the "Email Extension Plugin" in Jenkins.

### Step-by-Step Guide to Set Up Email Notifications with Log Snippets

#### 1. Install the Email Extension Plugin
First, you need to install the Email Extension Plugin in Jenkins.

1. **Navigate to Jenkins Dashboard:**
   - Go to `Manage Jenkins` > `Manage Plugins`.

2. **Install the Plugin:**
   - In the `Available` tab, search for "Email Extension Plugin".
   - Select it and click `Install without restart` or `Download now and install after restart`.

#### 2. Configure SMTP Settings
Next, configure Jenkins to send emails via your SMTP server.

1. **Navigate to Jenkins Configuration:**
   - Go to `Manage Jenkins` > `Configure System`.

2. **Scroll Down to the E-mail Notification Section:**
   - Enter your SMTP server details (e.g., SMTP server, port, username, password).
   - Test the configuration by clicking `Test configuration by sending test e-mail`.

3. **Scroll Down to Extended E-mail Notification:**
   - Similarly, enter the SMTP server details here.
   - Ensure that the `Default Content Type` is set to `HTML (text/html)` if you plan to include HTML content in your emails.

#### 3. Configure Job to Send Emails
Now, configure your Jenkins job to send email notifications with log snippets.

1. **Open Your Jenkins Job:**
   - Navigate to the specific job you want to configure.

2. **Add Post-Build Action:**
   - Scroll down to the `Post-build Actions` section.
   - Click `Add post-build action` and select `Editable Email Notification`.

3. **Configure Email Triggers:**
   - Under `Triggers`, add triggers like `Always`, `Failure`, `Success`, etc., depending on when you want the email to be sent.
   - For each trigger, click `Advanced...` to customize the email content.

4. **Customize Email Content:**
   - In the `Default Content` field, you can include predefined tokens and custom messages. Here are some useful tokens:
     - `${BUILD_LOG}`: Full build log.
     - `${BUILD_LOG_REGEX, regex=".*", linesBefore=0, linesAfter=0, maxMatches=0, showTruncatedLines=false, escapeHtml=false}`: Filtered build log based on a regular expression.
     - `${PROJECT_NAME}`, `${BUILD_NUMBER}`, `${BUILD_URL}`, etc.: Other useful project and build information.

   Example of an email template:
   ```html
   <h2>Jenkins Build Notification</h2>
   <p>Project: ${PROJECT_NAME}</p>
   <p>Build Number: ${BUILD_NUMBER}</p>
   <p>Status: ${BUILD_STATUS}</p>
   <p>Build URL: <a href="${BUILD_URL}">${BUILD_URL}</a></p>
   
   <h3>Build Log:</h3>
   <pre>${BUILD_LOG, maxLines=500}</pre>
   ```

   - Adjust the `maxLines` parameter to control how much of the log is included in the email.

5. **Specify Recipients:**
   - In the `Recipients` field, specify the email addresses of the developers who should receive the notifications.
   - You can also use environment variables or other dynamic values to specify recipients.

6. **Save the Job Configuration:**(#environment-values)
   - Click `Save` to apply the changes.

#### 4. Test the Setup
To ensure everything works as expected:
## Installation
Follow these steps to install.
1. **Trigger a Build:**
   - Manually trigger a build or wait for an automatic trigger.

2. **Check Emails:**
   - Check the specified email addresses to see if they received the notification with the log snippet.

3. **Verify Content:**
   - Open the email and verify that it contains the correct build information and log snippet.

### Additional Tips
- **Security:** Ensure that the SMTP credentials and any sensitive information are stored securely. Consider using Jenkins credentials store for managing passwords.
- **Log Size:** If logs are too large, consider using filters or truncating them to prevent excessively long emails.
- **Customization:** Customize the email templates further to include additional context or links to relevant resources.

# Jenkins Pipeline Configuration Guide

This document provides guidance on configuring and troubleshooting Jenkins pipelines.



## 1. Setting Up Environment Variables {#environment}
Jenkins requires you to specify an environment for your pipeline.

### 🔹 Allowed Values {#environment-values}
| Environment | Description |
|------------|-------------|
| `dev`      | Development environment |
| `staging`  | Staging environment for QA |
| `prod`     | Production environment |

💡 **Example Usage:**
```sh
ENVIRONMENT=staging


By following these steps, you can effectively notify developers about their Jenkins pipeline runs with relevant log snippets directly in their email inbox, keeping them informed without needing direct access to Jenkins.
[Go to Features](#features)
[Go to Installation](#installation)

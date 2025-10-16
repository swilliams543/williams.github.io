# williams.github.io
Fashion Blog

Look of the week
<img width="1920" height="3420" alt="image" src="https://github.com/user-attachments/assets/e53d79a8-cdfa-4a8d-90f5-8bb4ad881727" />
For this look I have paired a long, sleeveless colorful vest with dress pants. I paired it with a black cami. You can also pair this with a silky top as well. Since the color is bright, I paired this suit with brown, pointed toe sandals. This is a great look for work or an event. You are sure to have your own individually if you opt for this unique, chic look. For my hair, I wore a red bob which complements the color green. Whether you are going to work or going to an event, you're such to be unique with this summer, inspired look! 
#!/bin/bash

# Configuration Variables
# Replace these with your actual values
BUILD_COMMAND="npm run build"  # Command to build your project (e.g., for a React/Vue app)
LOCAL_BUILD_DIR="dist"         # Directory containing the built files (e.g., 'build', 'dist', 'public')
REMOTE_USER="user"             # SSH username for the server
REMOTE_HOST="your-server.com"  # Server hostname or IP
REMOTE_PATH="/var/www/html/mysite" # Directory on the server where files should go

# --- Deployment Steps ---

echo "🚀 Starting website deployment..."

# 1. Build the project locally
echo "🏗️  Running build command: $BUILD_COMMAND"
$BUILD_COMMAND

if [ $? -ne 0 ]; then
    echo "❌ Build failed. Aborting deployment."
    exit 1
fi

# 2. Sync files to the remote server using rsync
# -a: archive mode (recursively copy, preserve permissions)
# -z: compress file data during the transfer
# --delete: delete extraneous files from the destination (clean sync)
echo "📂 Syncing built files from $LOCAL_BUILD_DIR to $REMOTE_HOST:$REMOTE_PATH"
rsync -az --delete $LOCAL_BUILD_DIR/ $REMOTE_USER@$REMOTE_HOST:$REMOTE_PATH

if [ $? -ne 0 ]; then
    echo "❌ rsync failed. Check SSH connection and permissions."
    exit 1
fi

echo "✅ Deployment complete!"
2. GitHub Actions Workflow (CI/CD)
This is the industry-standard way to automate deployment. This YAML file lives in your repository under .github/workflows/main.yml.

Example: Deploying a Static Site (e.g., built with a framework like React/Vue) to an S3 Bucket
YAML

name: Deploy Website

on:
  push:
    branches:
      - main  # Trigger deployment when changes are pushed to the 'main' branch

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: ⚙️ Checkout repository code
        uses: actions/checkout@v4

      - name: 🛠️ Set up Node.js environment
        uses: actions/setup-node@v4
        with:
          node-version: '20' # Specify your required Node version

      - name: 📦 Install dependencies
        run: npm install

      - name: 🏗️ Build production files
        run: npm run build # Assumes your package.json has a 'build' script

      - name: 🚀 Deploy to AWS S3
        uses: jakejarvis/s3-sync-action@master
        with:
          args: --acl public-read --delete # S3 settings for static websites
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET_NAME }} # Bucket name
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }} # Stored in GitHub Secrets
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }} # Stored in GitHub Secrets
          SOURCE_DIR: 'dist' # The directory containing your built files (e.g., 'build' or 'dist')
Key Concepts Explained
CI/CD: Continuous Integration involves automatically building and testing code on every change. Continuous Deployment automatically deploys the successfully tested code to production.

GitHub Actions (.github/workflows/*.yml): A platform for running automated tasks based on repository events (like a push).

Jobs: A set of steps that execute on a runner (e.g., ubuntu-latest).

Steps: Individual tasks within a job (like actions/checkout@v4 or a run: npm install command).

secrets: Encrypted variables (like API keys or passwords) stored in your repository settings to keep sensitive data out of the workflow file.

rsync (in Bash): A powerful utility for efficiently transferring and synchronizing files, often preferred over plain scp for deployments.

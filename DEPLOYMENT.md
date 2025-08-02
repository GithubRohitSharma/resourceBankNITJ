# 🚀 Vercel Deployment Guide

## Prerequisites

1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com)
2. **GitHub Account**: Your code should be on GitHub
3. **MongoDB Atlas**: Set up a cloud MongoDB database
4. **Environment Variables**: Prepare your environment variables

## Step 1: Prepare Your Database

### MongoDB Atlas Setup
1. Go to [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Create a free cluster
3. Get your connection string
4. Whitelist your IP (or use `0.0.0.0/0` for all IPs)

## Step 2: Environment Variables Setup

Create a `.env` file locally for testing:

```env
PORT=8000
SECRET=your_super_secret_jwt_key_here
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/resourcebank
GOOGLE_DRIVE_CREDENTIALS={"type":"service_account",...}
FORGOTPASS=your_email_app_password
SUPPORT_MAIL=resourcebank.it@nitj.ac.in
```

## Step 3: Deploy to Vercel

### Method 1: Using Vercel CLI (Recommended)

1. **Install Vercel CLI**
   ```bash
   npm i -g vercel
   ```

2. **Login to Vercel**
   ```bash
   vercel login
   ```

3. **Deploy from your project directory**
   ```bash
   cd resourceBankNITJ
   vercel
   ```

4. **Follow the prompts**:
   - Link to existing project? → `N` (for first deployment)
   - Project name → `resource-bank-nitj`
   - Directory → `./` (current directory)
   - Override settings? → `N`

### Method 2: Using Vercel Dashboard

1. **Push your code to GitHub**
   ```bash
   git add .
   git commit -m "Prepare for Vercel deployment"
   git push origin main
   ```

2. **Connect to Vercel**:
   - Go to [vercel.com/dashboard](https://vercel.com/dashboard)
   - Click "New Project"
   - Import your GitHub repository
   - Select the repository

3. **Configure the project**:
   - Framework Preset: `Node.js`
   - Root Directory: `./`
   - Build Command: `npm run build`
   - Output Directory: `./`
   - Install Command: `npm install`

## Step 4: Configure Environment Variables

1. **In Vercel Dashboard**:
   - Go to your project settings
   - Navigate to "Environment Variables"
   - Add each variable from your `.env` file:

   ```
   SECRET=your_super_secret_jwt_key_here
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/resourcebank
   GOOGLE_DRIVE_CREDENTIALS={"type":"service_account",...}
   FORGOTPASS=your_email_app_password
   SUPPORT_MAIL=resourcebank.it@nitj.ac.in
   ```

2. **Deploy again** after adding environment variables:
   ```bash
   vercel --prod
   ```

## Step 5: Google Drive API Setup

1. **Create Google Cloud Project**:
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project
   - Enable Google Drive API

2. **Create Service Account**:
   - Go to "IAM & Admin" → "Service Accounts"
   - Create a new service account
   - Download the JSON credentials

3. **Share Google Drive folder**:
   - Create a folder in Google Drive
   - Share it with your service account email
   - Give it "Editor" permissions

4. **Add credentials to Vercel**:
   - Copy the entire JSON content
   - Add it as `GOOGLE_DRIVE_CREDENTIALS` environment variable

## Step 6: Email Configuration

1. **Gmail App Password**:
   - Enable 2-factor authentication on your Gmail
   - Generate an app password
   - Use it as `FORGOTPASS` environment variable

2. **Test email functionality** after deployment

## Step 7: Verify Deployment

1. **Check your deployment URL** (e.g., `https://resource-bank-nitj.vercel.app`)

2. **Test all features**:
   - User registration/login
   - File upload/download
   - Admin dashboard
   - Email functionality

## Troubleshooting

### Common Issues:

1. **Database Connection Error**:
   - Check MongoDB URI format
   - Ensure IP whitelist includes Vercel's IPs
   - Verify database name and credentials

2. **File Upload Issues**:
   - Check Google Drive API credentials
   - Verify folder permissions
   - Check environment variables

3. **Email Not Working**:
   - Verify Gmail app password
   - Check `FORGOTPASS` environment variable
   - Test email configuration

4. **Build Errors**:
   - Check `vercel.json` configuration
   - Verify all dependencies in `package.json`
   - Check for syntax errors

### Debug Commands:

```bash
# Check Vercel logs
vercel logs

# Redeploy with fresh build
vercel --prod --force

# Check environment variables
vercel env ls
```

## Post-Deployment

1. **Set up custom domain** (optional):
   - Go to project settings in Vercel
   - Add your custom domain
   - Configure DNS settings

2. **Monitor performance**:
   - Use Vercel Analytics
   - Monitor error logs
   - Check database performance

3. **Set up automatic deployments**:
   - Connect to GitHub
   - Enable automatic deployments on push

## Security Notes

- ✅ Use strong JWT secrets
- ✅ Enable MongoDB authentication
- ✅ Use environment variables for all secrets
- ✅ Regularly rotate API keys
- ✅ Monitor access logs

---

**Your app should now be live at**: `https://your-project-name.vercel.app` 
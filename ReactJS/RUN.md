# Deploying a React.js Project to cPanel

This guide provides steps to deploy a React.js project to a shared hosting environment via cPanel, either on a main domain or a subdomain.

## Steps for Deployment

### 1. Build the Project for Production
   - Run the following command to build the project:
     ```bash
     npm run build
     ```
   - This will generate a `dist` folder containing the production-ready static files.

### 2. Prepare the `dist` Folder for Upload
   - Compress the `dist` folder into a `.zip` file (e.g., `dist.zip`) so it can be easily uploaded.

### 3. Upload the `.zip` File to cPanel
   - Log in to **cPanel**.
   - Navigate to **File Manager** and open the directory where you want to deploy the project:
     - For a main domain, this is usually `/public_html`.
     - For a subdomain, it’s usually something like `/public_html/subdomain` or `/home/username/subdomain`.
   - Upload the `dist.zip` file to this directory.

### 4. Extract and Organize the Files
   - Select the uploaded `dist.zip` file and **Extract** it within **File Manager**.
   - You’ll see a new `dist` folder after extraction.
   - Move all files and folders inside the `dist` folder directly to the root directory of your domain or subdomain.
   - Delete the now-empty `dist` folder and the original `dist.zip` file to keep your directory clean.

### 5. Set Up `.htaccess` for React Router
   - In the root directory of your domain or subdomain, create a new file called `.htaccess` (if it doesn’t exist already).
   - Add the following code to handle client-side routing:

     ```apache
     <IfModule mod_rewrite.c>
       RewriteEngine On
       RewriteBase /
       RewriteRule ^index\.html$ - [L]
       RewriteCond %{REQUEST_FILENAME} !-f
       RewriteCond %{REQUEST_FILENAME} !-d
       RewriteCond %{REQUEST_FILENAME} !-l
       RewriteRule . /index.html [L]
     </IfModule>
     ```

   - Save the file.

### 6. Test the Deployment
   - Visit your domain or subdomain in a browser.
   - You should now see your React.js project running!

### Troubleshooting
If you encounter any issues, double-check that:
- All files are in the root directory (not nested in a `dist` folder).
- The `.htaccess` file is in the correct location and configured as shown above.

Your React.js project should now be successfully deployed and accessible on your domain or subdomain.

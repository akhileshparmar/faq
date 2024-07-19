# Deploy a React application on Netlify

To deploy a React application on Netlify using the CLI, along with setting up redirect and rewrite rules, follow these steps:

1. **Install the Netlify CLI**:
   Ensure you have Node.js installed, then install the Netlify CLI globally:

   ```bash
   npm install -g netlify-cli
   ```

2. **Log in to Netlify**:
   Log in to your Netlify account using the CLI:

   ```bash
   netlify login
   ```

3. **Create a production build**:
   Navigate to your React project directory and create a production build:

   ```bash
   npm run build
   ```

4. **Create a `_redirects` file**:
   In your `public` directory, create a `_redirects` file to handle redirect and rewrite rules. For example, to handle client-side routing, add the following:

   ```
   /* /index.html 200
   ```

5. **Deploy to Netlify**:
   Deploy your site using the `netlify deploy` command. You will be prompted to select a site or create a new one.

   ```bash
   netlify deploy
   ```

   - When prompted for the deploy path, enter `build` (the directory where your production build is located).

6. **Deploy to production**:
   If you are satisfied with the deploy preview, you can deploy to production:

   ```bash
   netlify deploy --prod
   ```

7. **Push your changes (optional)**:
   If you haven't already pushed your changes to your version control system (like GitHub), do so:
   ```bash
   git add .
   git commit -m "Deploy React app to Netlify with redirect and rewrite rules"
   git push origin main
   ```

Here's a step-by-step example:

1. Install Netlify CLI:

   ```bash
   npm install -g netlify-cli
   ```

2. Log in to Netlify:

   ```bash
   netlify login
   ```

3. Create a production build:

   ```bash
   npm run build
   ```

4. Create a `_redirects` file in the `public` directory with the following content:

   ```
   /* /index.html 200
   ```

5. Deploy to Netlify:

   ```bash
   netlify deploy
   ```

   - Select your site or create a new one.
   - Enter `build` when prompted for the deploy path.

6. Deploy to production:

   ```bash
   netlify deploy --prod
   ```

7. Push your changes (if needed):
   ```bash
   git add .
   git commit -m "Deploy React app to Netlify with redirect and rewrite rules"
   git push origin main
   ```

By following these steps, your React application will be deployed on Netlify with the specified redirect and rewrite rules, ensuring smooth handling of client-side routing.

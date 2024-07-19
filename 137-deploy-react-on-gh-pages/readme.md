# Deploy a React application to GitHub Pages

To deploy a React application to GitHub Pages using the command line, follow these steps:

1. **Install GitHub Pages package**:
   Navigate to your React project directory and install the `gh-pages` package:

   ```bash
   npm install gh-pages --save-dev
   ```

2. **Update `package.json`**:
   Add the following properties to your `package.json` file:

   - Add a `homepage` field with the URL to your GitHub Pages site:
     ```json
     "homepage": "https://<username>.github.io/<repository-name>"
     ```
   - Add `predeploy` and `deploy` scripts:
     ```json
     "scripts": {
       "predeploy": "npm run build",
       "deploy": "gh-pages -d build",
       // other scripts
     }
     ```

3. **Create a production build**:
   Generate the production build of your React application:

   ```bash
   npm run build
   ```

4. **Deploy to GitHub Pages**:
   Use the `gh-pages` command to deploy your application:

   ```bash
   npm run deploy
   ```

5. **Push your changes**:
   Commit and push your changes to your repository:
   ```bash
   git add .
   git commit -m "Deploy React app to GitHub Pages"
   git push origin main
   ```

After following these steps, your React application should be deployed to GitHub Pages and accessible at the URL specified in the `homepage` field.

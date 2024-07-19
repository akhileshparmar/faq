# Deploy Next.js Application on Vercel

To deploy the latest version of a Next.js application on Vercel using the CLI, follow these steps:

1. **Install the Vercel CLI**:
   Make sure you have Node.js installed, then install the Vercel CLI globally:

   ```bash
   npm install -g vercel
   ```

2. **Log in to Vercel**:
   Log in to your Vercel account using the CLI:

   ```bash
   vercel login
   ```

3. **Initialize a new Next.js project (if you don't already have one)**:
   You can skip this step if you already have a Next.js project. If not, create a new Next.js project:

   ```bash
   npx create-next-app@latest
   cd your-project-name
   ```

4. **Deploy to Vercel**:
   In your Next.js project directory, run the following command to deploy:

   ```bash
   vercel
   ```

   - Follow the prompts to set up and deploy your project. This includes selecting a scope, linking or creating a new project, and configuring project settings.

5. **Deploy to production**:
   Once the initial deployment is complete, you can deploy to production with:

   ```bash
   vercel --prod
   ```

6. **Push your changes (optional)**:
   If you haven't already pushed your changes to your version control system (like GitHub), do so:
   ```bash
   git add .
   git commit -m "Deploy Next.js app to Vercel"
   git push origin main
   ```

Here's a step-by-step example:

1. Install Vercel CLI:

   ```bash
   npm install -g vercel
   ```

2. Log in to Vercel:

   ```bash
   vercel login
   ```

3. (Optional) Initialize a new Next.js project:

   ```bash
   npx create-next-app@latestis
   cd your-project-name
   ```

4. Deploy to Vercel:

   ```bash
   vercel
   ```

   - Follow the prompts to configure your project.

5. Deploy to production:

   ```bash
   vercel --prod
   ```

6. Push your changes (if needed):
   ```bash
   git add .
   git commit -m "Deploy Next.js app to Vercel"
   git push origin main
   ```

By following these steps, your Next.js application will be deployed on Vercel using the latest version.

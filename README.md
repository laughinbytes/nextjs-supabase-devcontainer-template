# Next.js + Supabase Dev Container Template

This repository provides a reusable development environment configuration for projects based on Next.js, TypeScript, pnpm, and Supabase. It standardizes the development setup for VS Code Dev Containers and Gitpod using a `.devcontainer/devcontainer.json` file.

## ✨ Environment Features

- **Base System**: Ubuntu 22.04 LTS
- **Node.js**: LTS version managed via nvm (supports `.nvmrc`)
- **Package Manager**: pnpm (latest version)
- **TypeScript**: (To be installed by the specific project)
- **Docker & Docker Compose**: Provided via Docker-in-Docker feature
- **Supabase CLI**: Required for local development; install it manually by running `npm install -g supabase` inside the container.
- **Common Utilities**: Git, Zsh, etc.
- **VS Code Integration**:
  - Recommended extensions:
    - ESLint and Prettier for code formatting
    - Docker for container management
    - Prisma for database schema
    - Tailwind CSS IntelliSense
    - GitHub Copilot
    - Pretty TypeScript Errors
    - Supabase
  - Preset editor configurations (e.g., format on save, single quotes)
- **Port Forwarding**: Pre-configured for Next.js and local Supabase services
- **Git Configuration**: Attempts to automatically set global Git `user.name` and `user.email` within the container using `GIT_AUTHOR_NAME` and `GIT_AUTHOR_EMAIL` environment variables (Gitpod sets these automatically).

## 🚀 How to Use This Environment Configuration

This repository itself is **not a full project boilerplate**, but rather provides a `.devcontainer` setup that can be added to any project to quickly establish a consistent development environment.

### Option 1: For a Brand New Project

1.  **Create your Project Repository**: Create your new project repository on GitHub.
2.  **Initialize Project in Gitpod/Dev Container**:
    - **Gitpod**: Open your newly created (empty) repository's Gitpod workspace (e.g., by prefixing the GitHub URL with `gitpod.io#`).
    - **VS Code (Local)**: Clone your new empty project repository locally, then open it in VS Code.
3.  **Add This Dev Environment Configuration**:
    - In the root of your new project, create a `.devcontainer` directory.
    - Copy the `devcontainer.json` file from this `nextjs-supabase-devcontainer-template` repository into your new project's `.devcontainer/` directory.
4.  **Reload/Reopen in Dev Environment**:
    - **Gitpod**: After adding `.devcontainer/devcontainer.json` (e.g., by committing and pushing it, or creating it directly in the Gitpod workspace), Gitpod may prompt you to rebuild or will use it on the next workspace start.
    - **VS Code**: VS Code should detect the `devcontainer.json` file and prompt you to "Reopen in Container".
5.  **Initialize Your Project Files Inside the Dev Environment**:
    - Open a terminal within the activated dev environment.
    - Run your project creation commands, for example:
      ```bash
      pnpm create next-app . --ts
      # Follow the prompts from create-next-app
      ```
    - Install dependencies (if not automatically handled after `package.json` creation by `postCreateCommand` or if you need to update):
      ```bash
      pnpm install --shamefully-hoist
      ```
    - Initialize Supabase for your project (if using Supabase):
      ```bash
      supabase init
      ```
      This will create the `supabase/` directory and `config.toml`. Remember to commit these to your project.
    - Start Supabase services as needed:
      ```bash
      supabase start
      ```

### Option 2: For an Existing Project

1.  **Copy `.devcontainer` Folder**: Copy the entire `.devcontainer` folder (containing `devcontainer.json`) from this `nextjs-supabase-devcontainer-template` repository into the root directory of your existing project.
2.  **Commit Changes**: Add the `.devcontainer` folder to your Git tracking and commit the changes to your project repository.
3.  **Open Project**:
    - **Gitpod**: Open your project in Gitpod. It will automatically detect and use the new `.devcontainer` configuration.
    - **VS Code (Local)**: Open your project in VS Code. It should detect the Dev Container configuration and prompt you to "Reopen in Container".

## 🛠️ Inside the Development Environment

Once the environment is up and running:

- **Dependencies**: The `postCreateCommand` in `devcontainer.json` attempts to run `pnpm install` if a `package.json` is present. You can always run it manually if needed.
- **Project Initialization**: The `postStartCommand` will display a message reminding you to initialize your project and start services manually. You can follow these steps:
  - Initialize your Next.js project if needed: `pnpm create next-app . --ts`
  - Start your development server: `pnpm dev`
- **Supabase**:
  - If your project's `supabase/` directory doesn't exist, run `supabase init` in the terminal.
  - Start Supabase services manually with `supabase start` when needed
  - Access the local Supabase Studio (dashboard) typically at `http://localhost:54323` (or the equivalent forwarded port in Gitpod).
- **Next.js**:
  - Start your Next.js development server with `pnpm dev`
  - Your Next.js application will typically be available at `http://localhost:3000` (or the equivalent forwarded port in Gitpod).
- **Environment Variables**: For your Next.js application to connect to Supabase, create a `.env.local` file in your project root and configure `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`. Obtain these values from the output of `supabase status` or `supabase start`. Example:
  ```env
  NEXT_PUBLIC_SUPABASE_URL=http://localhost:54321
  NEXT_PUBLIC_SUPABASE_ANON_KEY=your-local-anon-key-from-supabase-status
  ```

## 📝 Notes

- If using VS Code Dev Containers locally, ensure Docker Desktop is installed and running.
- This `devcontainer.json` includes VS Code extensions for ESLint and Prettier. For them to function correctly with your project's preferred styles, you'll need to add the corresponding configuration files (e.g., `.eslintrc.json`, `.prettierrc.json`) within each specific project that uses this environment.

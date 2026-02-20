# vue-login-form

> A quick login form credential checker built with Vue 3 and Vite.

[![Vue](https://img.shields.io/badge/Vue-3.x-4FC08D?logo=vue.js)](https://vuejs.org/)
[![Vite](https://img.shields.io/badge/Vite-latest-646CFF?logo=vite)](https://vitejs.dev/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?logo=javascript)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## About the Project

**vue-login-form** is a lightweight, client-side login form application that validates user credentials and makes a pass/fail decision on whether to grant access to a protected dashboard. It is designed as a clean, minimal starting point for authentication UI flows using Vue 3's Composition API and Vue Router.

When a user submits their credentials, the form validates the input fields in real time, then routes the user to a dashboard on success or displays an error on failure — all without a backend dependency, making it ideal for rapid prototyping and UI testing.

---

## Features

- **Input Validation** — Real-time field-level validation for username and password inputs, including checks for empty fields, minimum length, and format requirements.
- **Access Decision** — Credential checker logic that evaluates submitted credentials and decides whether to grant or deny access.
- **Client-Side Routing** — Seamless, page-reload-free navigation between the Login and Dashboard views via Vue Router.
- **Dashboard View** — A post-login dashboard displaying user stats and a functional logout button that redirects back to the login screen.
- **Responsive Design** — Clean, minimal CSS styling that works across desktop and mobile screen sizes.

---

## Tech Stack

| Technology | Purpose |
|---|---|
| [Vue 3](https://vuejs.org/) | Frontend framework (Composition API + `<script setup>` SFCs) |
| [Vite](https://vitejs.dev/) | Build tool and dev server |
| [Vue Router](https://router.vuejs.org/) | Client-side routing |
| [JavaScript (ES6+)](https://developer.mozilla.org/en-US/docs/Web/JavaScript) | Application logic |

---

## Project Structure

```
vue-login-app/
├── public/                  # Static assets
├── src/
│   ├── main.js              # Vue entry point — mounts app and registers router
│   ├── App.vue              # Root component containing <RouterView />
│   ├── router/
│   │   └── index.js         # Route definitions (/ → LoginForm, /dashboard → Dashboard)
│   └── components/
│       ├── LoginForm.vue    # Login UI with input validation and navigation logic
│       └── Dashboard.vue    # Post-login view with stats display and logout
├── index.html               # HTML entry point
├── vite.config.js           # Vite configuration
├── package.json             # Project dependencies and scripts
└── .gitignore
```

---

## Installation

### Prerequisites

Ensure the following are installed on your system before proceeding:

- **Node.js** v16 or higher — [Download here](https://nodejs.org/)
- **npm** v7 or higher (bundled with Node.js) — or alternatively **yarn** / **pnpm**
- A modern web browser (Chrome, Firefox, Edge, Safari)
- A code editor such as [VS Code](https://code.visualstudio.com/) (recommended, with the [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) extension for Vue support)

### Steps

1. **Clone the repository**

   ```bash
   git clone https://github.com/morrismutiso/vue-login-form.git
   cd vue-login-form
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Start the development server**

   ```bash
   npm run dev
   ```

4. **Open in your browser**

   Navigate to `http://localhost:5173` (or the port shown in your terminal).

---

## Usage

### Running the App

```bash
# Development server with hot module replacement
npm run dev

# Build for production
npm run build

# Preview the production build locally
npm run preview
```

### Basic Flow

1. Open the app in your browser — you will land on the **Login Form** page.
2. Enter a username and password in the respective fields.
3. The form validates your input as you type:
   - Fields cannot be empty.
   - Password must meet the minimum length requirement.
4. Click **Login** to submit:
   - **Valid credentials** → you are routed to the **Dashboard**.
   - **Invalid credentials** → an error message is displayed on the form.
5. On the Dashboard, click **Logout** to return to the Login page.

### Example Credential Check

The credential checker in `LoginForm.vue` compares submitted values against a set of accepted credentials. To test the app out of the box:

```
Username: admin
Password: password123
```

> You can update the accepted credentials directly in `LoginForm.vue` to match your needs (see [Configuration](#configuration)).

---

## Configuration

### Changing Accepted Credentials

Open `src/components/LoginForm.vue` and locate the credential validation logic. Update the hardcoded values (or replace the check with an API call) to configure which credentials are accepted:

```js
// Example inside LoginForm.vue
const validUsername = 'admin'
const validPassword = 'password123'

function handleLogin() {
  if (username.value === validUsername && password.value === validPassword) {
    router.push('/dashboard')
  } else {
    errorMessage.value = 'Invalid username or password.'
  }
}
```

### Changing Routes

Routes are defined in `src/router/index.js`. You can add, remove, or rename routes here:

```js
const routes = [
  { path: '/', component: LoginForm },
  { path: '/dashboard', component: Dashboard },
]
```

### Vite Configuration

The `vite.config.js` file at the project root controls the build tool settings. You can change the dev server port, set a base URL for deployment, and add plugins here:

```js
// vite.config.js
export default defineConfig({
  plugins: [vue()],
  server: {
    port: 5173, // Change this to use a different port
  },
})
```

---

## Troubleshooting

**`npm install` fails or throws dependency errors**
Ensure you are using Node.js v16 or higher. Run `node -v` to check your version. If needed, use [nvm](https://github.com/nvm-sh/nvm) to switch versions.

**Port 5173 is already in use**
Either stop the process using that port, or configure a different port in `vite.config.js` under `server.port`.

**The page is blank after navigating to `/dashboard` directly**
Direct URL access to child routes may fail if the app is deployed on a static host without proper redirect rules. Ensure your hosting provider is configured to redirect all routes to `index.html`. For local development, this is handled automatically by Vite.

**Changes to `.vue` files are not reflected in the browser**
Hot Module Replacement (HMR) should handle this automatically. If it stops working, try restarting the dev server with `npm run dev`.

**Volar / VS Code IntelliSense not working for Vue files**
Make sure the [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) extension is installed and that the deprecated Vetur extension is disabled to avoid conflicts.

---

## Contributing

Contributions are welcome! To get started:

1. Fork the repository on GitHub.
2. Create a new feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes and commit them with a clear message:
   ```bash
   git commit -m "feat: add remember-me checkbox to login form"
   ```
4. Push your branch to your fork:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a **Pull Request** against the `main` branch of this repository.

Please ensure your code follows the existing style conventions and that all validation logic remains in `LoginForm.vue` to keep the project structure consistent.

---

## License

This project is licensed under the **MIT License**. You are free to use, modify, and distribute this project for personal or commercial purposes.

See the [LICENSE](LICENSE) file for full details.

---

*Built with Vue 3 + Vite · [github.com/morrismutiso/vue-login-form](https://github.com/morrismutiso/vue-login-form)*
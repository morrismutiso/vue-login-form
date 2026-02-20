<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

// ── ROUTER ─────────────────────────────
const router = useRouter()

// ── YOUR VARIABLES (nouns) ──────────────
const email = ref('')
const password = ref('')
const rememberMe = ref(false)
const errorMessage = ref('')
const successMessage = ref('')

// ── YOUR METHODS (verbs) ────────────────
function validateEmail() {
  if (!email.value) {
    errorMessage.value = 'Email is required'
    return false
  } else if (!email.value.includes('@')) {
    errorMessage.value = 'Email must contain @'
    return false
  }
  return true
}

function validatePassword() {
  if (!password.value) {
    errorMessage.value = 'Password is required'
    return false
  } else if (password.value.length < 6) {
    errorMessage.value = 'Password must be at least 6 characters'
    return false
  }
  return true
}

function submitForm() {
  errorMessage.value = ''
  successMessage.value = ''
  const emailValid = validateEmail()
  const passwordValid = validatePassword()

  if (emailValid && passwordValid) {
    router.push({
      path: '/dashboard',
      query: { email: email.value }
    })
  }
}
</script>

<template>
  <div class="login-container">

    <h2>Sign In</h2>

    <!-- EMAIL FIELD -->
    <div class="form-group">
      <label>Email Address</label>
      <input
        type="email"
        placeholder="you@example.com"
        v-model="email"
      />
    </div>

    <!-- PASSWORD FIELD -->
    <div class="form-group">
      <label>Password</label>
      <input
        type="password"
        placeholder="Enter your password"
        v-model="password"
      />
    </div>

    <!-- REMEMBER ME -->
    <div class="form-group">
      <input type="checkbox" id="remember" v-model="rememberMe" />
      <label for="remember">Remember me</label>
    </div>

    <!-- ERROR MESSAGE -->
    <p v-if="errorMessage">⚠ {{ errorMessage }}</p>

    <!-- SUCCESS MESSAGE -->
    <p v-if="successMessage">{{ successMessage }}</p>

    <!-- SUBMIT BUTTON -->
    <button type="button" @click="submitForm">Sign In</button>

  </div>
</template>

<style scoped>
.login-container {
  max-width: 400px;
  margin: 60px auto;
  padding: 2rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  font-family: sans-serif;
}

h2 {
  margin-bottom: 1.5rem;
  color: #333;
  text-align: center;
}

.form-group {
  margin-bottom: 1.2rem;
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

label {
  font-size: 0.85rem;
  font-weight: 500;
  color: #555;
}

input[type="email"],
input[type="password"] {
  padding: 0.7rem 1rem;
  border: 1.5px solid #ddd;
  border-radius: 6px;
  font-size: 0.95rem;
  outline: none;
  transition: border 0.2s;
}

input[type="email"]:focus,
input[type="password"]:focus {
  border-color: #41b883;
}

button {
  width: 100%;
  padding: 0.8rem;
  background: #41b883;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.2s;
}

button:hover {
  background: #2d7a5c;
}

p {
  font-size: 0.85rem;
  padding: 0.6rem 0.8rem;
  border-radius: 5px;
  margin-bottom: 0.8rem;
}

p:has(span), p {
  background: #fdedec;
  color: #c0392b;
}

p:last-of-type {
  background: #eafaf1;
  color: #1e5631;
}
</style>
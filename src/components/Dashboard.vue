<script setup>
import { useRoute, useRouter } from 'vue-router'

// ── ROUTER ─────────────────────────────
const route = useRoute()
const router = useRouter()

// ── GET EMAIL FROM URL ──────────────────
const email = route.query.email

// ── METHODS ────────────────────────────
function logout() {
  router.push('/')
}
</script>

<template>
  <div class="dashboard-container">

    <!-- HEADER -->
    <div class="dashboard-header">
      <h2>Dashboard</h2>
      <button @click="logout">Logout</button>
    </div>

    <!-- WELCOME CARD -->
    <div class="welcome-card">
      <h3>Welcome back!</h3>
      <p>Logged in as <strong>{{ email }}</strong></p>
    </div>

    <!-- STATS CARDS -->
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-number">24</div>
        <div class="stat-label">Projects</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">8</div>
        <div class="stat-label">Tasks Due</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">3</div>
        <div class="stat-label">Messages</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">92%</div>
        <div class="stat-label">Completion</div>
      </div>
    </div>

  </div>
</template>

<style scoped>
.dashboard-container {
  max-width: 800px;
  margin: 40px auto;
  padding: 2rem;
  font-family: sans-serif;
}

.dashboard-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #ddd;
}

.dashboard-header h2 {
  color: #333;
  font-size: 1.8rem;
}

.dashboard-header button {
  padding: 0.5rem 1.2rem;
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background 0.2s;
}

.dashboard-header button:hover {
  background: #c0392b;
}

.welcome-card {
  background: #41b883;
  color: white;
  padding: 1.5rem 2rem;
  border-radius: 8px;
  margin-bottom: 2rem;
}

.welcome-card h3 {
  font-size: 1.3rem;
  margin-bottom: 0.4rem;
}

.welcome-card p {
  font-size: 0.95rem;
  opacity: 0.9;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

.stat-card {
  background: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 1.5rem;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
  transition: transform 0.2s;
}

.stat-card:hover {
  transform: translateY(-3px);
}

.stat-number {
  font-size: 2rem;
  font-weight: 700;
  color: #41b883;
  margin-bottom: 0.4rem;
}

.stat-label {
  font-size: 0.85rem;
  color: #888;
}
</style>
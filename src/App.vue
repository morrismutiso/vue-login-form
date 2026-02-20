<script setup>
</script>

<template>
  <RouterView />
</template>

<style scoped>
</style>
```

**Notice:**
- removed the `LoginForm` import
- removed `<LoginForm />` 
- added `<RouterView />` — the router's placeholder

Save with `Ctrl + S` and try visiting both URLs:
```
http://localhost:5173/
http://localhost:5173/dashboard

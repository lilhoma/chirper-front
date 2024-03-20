<template>
  <Title>{{ title }}</Title>
  <div class="bg-gray-100 min-h-screen text-gray-900">
    <nav class="bg-white shadow text-lg px-6 py-6">
      <div class="container max-auto flex items-center justify-between px-6">
        <div>
          <NuxtLink to="/" class="font-bold">Chirper</NuxtLink>
        </div>
        <div>
          <ul class="flex space-x-12">
            <li>
              <NuxtLink to="/">Chirps</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/register">Register</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/login">Log In</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/my-info">My Dashboard</NuxtLink>
            </li>
            <li><a href="#" @click.prevent="logout">Logout</a></li>
          </ul>
        </div>
      </div>
    </nav>
    <slot />
  </div>
</template>

<script setup>
const title = useState('title', () => "Chirp");
const { $apiFetch } = useNuxtApp()
async function logout() {
  try {
    await $apiFetch('/logout', {
      method: 'POST',
    })
  } catch (err) {
    console.log(err.data)
  } finally {
    window.location.pathname = '/'
  }
}
</script>
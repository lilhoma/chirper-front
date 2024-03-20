<template>
  <Title>{{ title }}</Title>
  <div class="bg-gray-100 min-h-screen text-gray-900">
    <nav class="bg-violet-300 shadow text-lg px-6 py-6">
      <div class="container max-auto flex items-center justify-between px-6">
        <div>
          <NuxtLink to="/" class="font-bold">Chirper</NuxtLink>
        </div>
        <div>
          <ClientOnly>
            <ul class="flex space-x-12">
              <li >
                <NuxtLink to="/">Chirps</NuxtLink>
              </li>
              <li v-if="!isLoggedIn">
                <NuxtLink to="/register">Register</NuxtLink>
              </li>
              <li v-if="!isLoggedIn">
                <NuxtLink to="/login">Log In</NuxtLink>
              </li>
              <li v-if="isLoggedIn">
                <NuxtLink to="/my-info">My Dashboard</NuxtLink>
              </li>
              <li><a href="#" @click.prevent="logout">Logout</a></li>
            </ul>
          </ClientOnly>
        </div>
      </div>
    </nav>
    <slot />
  </div>
</template>

<script setup>
const title = useState('title', () => "Chirp");
const { $apiFetch } = useNuxtApp();
const { removeUser, isLoggedIn} = useAuth();

async function logout() {
  try {
    await $apiFetch('/logout', {
      method: 'POST',
    })
  } catch (err) {
    console.log(err.data)
  } finally {
    removeUser();
    window.location.pathname = '/'
  }
}
</script>

<style>
  .router-link-active{
    font-weight: bold;
  }
</style>
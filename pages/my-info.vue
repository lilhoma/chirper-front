<template>
    <div class="container mx-auto w-1/2 py-8">
        <Title>My Info | {{ title }}</Title>
        <div>
            <div>Name: {{ user?.name }}</div>
            <div>Email: {{ user?.email }}</div>
        </div>

        <div class="mt-4">
            <h2 class="font-bold">My Chirps</h2>
            <ul>
                <li v-for="chirp in chirps" :key="chirp.id">{{ chirp.message }}</li>
            </ul>
        </div>
    </div>
</template>

<script setup>

const title = useState('title');

const {$apiFetch} = useNuxtApp();
const user = ref(null);
const chirps = ref([]);

onMounted(async() => {
    user.value = await $apiFetch('api/user');
   
    chirps.value = await $apiFetch('api/user/chirps');
    
});

</script>
<template>
  <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
    <form action="#" @submit.prevent="createChirp">
      <label for="body" class="block font-semibold"> New Chirp</label>
      <textarea
        v-model="message"
        name="body"
        id="body"
        rows="5"
        class="block w-full border border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
      ></textarea>
      <!-- errors -->
      <ul
        v-if="errors.length > 0"
        class="list-disc list-inside text-sm text-red-600"
      >
        <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
      </ul>

      <button
        type="submit"
        class="uppercase text-white bg-blue-400 border border-gray-500 hover:bg-blue-600 px-4 py-1 rounded-md mt-2"
      >
        Chirp
      </button>
      <span v-if="isLoading">Loading...</span>
    </form>

    <div>
    <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
      <Chirp v-for="chirpT in chirps" :key="chirpT.id" :chirp="chirpT" />
    </div>
  </div>
  </div>
</template>

<script setup>
const message = ref("");
const errors = ref([]);
const isLoading = ref(false);
const router = useRouter();

const { $apiFetch } = useNuxtApp();

const chirps = await $apiFetch("/api/chirps");


async function createChirp() {
  try {
    isLoading.value = true;
    const chirp = await useNuxtApp().$apiFetch(`/api/chirp`, {
      method: "POST",
      body: {
        message: message.value,
      },
    });

    isLoading.value = false;
    message.value = "";
    // alert("Sending Chirp");
    window.location.pathname = "/";
  } catch (err) {
    console.log(err.data);
    errors.value = Object.values(err.data.errors).flat();
    isLoading.value = false;
  }
}
</script>

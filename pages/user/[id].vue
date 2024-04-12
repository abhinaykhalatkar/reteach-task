<template>
  <article>
    <h1>User profile</h1>
    <div v-if="user">
      <h3>Name: {{ user.name }}</h3>
      <p>Email: {{ user.email }}</p>
      <p>Username: {{ user.username }}</p>
      <p>Phone: {{ user.phone }}</p>
      <p>Website: {{ user.website }}</p>
      <p>Address: {{ user.address.street }},{{ user.address.city }}, {{ user.address.zipcode }}</p>
    </div>
    <div v-else>
      Loading user profile...
    </div>
  </article>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const user = ref(null);

const router = useRouter();

useAsyncData(async () => {
  const idParam = router.currentRoute.value.params?.id;

  if (idParam) {
    try {
      const response = await fetch(`https://jsonplaceholder.typicode.com/users/${idParam}`);
      if (response.ok) {
        user.value = await response.json();
        console.log(user._rawValue)
      } else {
        throw new Error(`Failed to fetch (${response.status})`);
      }
    } catch (error) {
      console.error('Error fetching :', error);
    }
  }
});
</script>

<style scoped>
article {
  min-width: 200px;
}
</style>

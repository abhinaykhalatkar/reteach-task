<template>
  <AwesomeSection>
    <h2>Users List</h2>
    <input type="text" placeholder="Search..." v-model="search" />
    <ul v-for="user in filteredUsers" :key="user.id">
      <NuxtLink :to="`/user/${user.id}`" tag="li">
        <p>Name: {{ user.name }}</p>
        <p>Email: {{ user.email }}</p>
        <p>Username: {{ user.username }}</p>
      </NuxtLink>
    </ul>
  </AwesomeSection>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useAsyncData } from 'nuxt/app';

const search = ref('');
const users = ref(null);

useAsyncData(async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/users');
  users.value = await response.json();
});

const filteredUsers = computed(() => {
  if (!users.value) return [];
  return users.value.filter((user) =>
    user.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>

<style scoped>
ul {
  padding: 0;
  width: 100%;
  border-bottom: 2px solid black;
}

a {
  text-decoration: none;
  color: black;
}


@media (max-width: 768px) {

  section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  ul {
    text-align: center;

  }

  @media (max-width: 420px) {
    ul {
      border-radius: 5px;
      border-bottom: none;
      box-shadow: rgb(80, 86, 90) 2px 4px 10px 0px
    }
  }
}
</style>
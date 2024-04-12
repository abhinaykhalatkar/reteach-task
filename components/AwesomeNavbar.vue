<template>
  <nav>
    Navigation
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <NuxtLink :to="`/`" :key="index">
          Home {{ index + 1 }}
        </NuxtLink>
      </li>
    </ul>
  </nav>
</template>
<script setup>
const items = new Array(10).fill(null);
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;

}

li {
  flex: 1 0 auto;
  box-sizing: border-box;
  text-align: center;
}

a {
  color: rgb(0, 0, 0);
  text-decoration: none;

}

a:hover {
  text-decoration: underline;
}

@media (max-width: 768px) {
  li {
    flex-basis: calc(20% - 20px);
  }
}

@media (max-width: 420px) {
  li {
    flex-basis: calc(50% - 20px);
  }
}
</style>

<template>
  <main class="my-5 px-3 lg:grid lg:grid-cols-3 gap-8">
    <div class="h-96 mb-5 bg-purple-300"></div>

    <div class="lg:col-span-2 mb-5 bg-purple-300">
      <UserTable />
    </div>
  </main>
</template>

<script>
import UserTable from './UserTable.vue'

export default {
  components: {
    UserTable,
  }
};
</script>

<style>
</style>
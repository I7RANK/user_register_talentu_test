<template>
  <main class="my-5 px-3 lg:grid lg:grid-cols-3 gap-8">
    <div class="h-96 mb-5 rounded-2xl shadow-md py-5">
      <UserForm />
    </div>

    <div class="lg:col-span-2 mb-5 rounded-2xl shadow-md py-5">
      <UserTable />
    </div>
  </main>
</template>

<script>
import UserTable from './UserTable.vue'
import UserForm from './UserForm.vue'

export default {
  components: {
    UserTable,
    UserForm,
  }
};
</script>

<style>
  main div {
    background: var(--background-secondary);
  }
</style>
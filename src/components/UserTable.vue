<template>
  <table class="user-table table-auto min-w-full rounded-t-2xl border-2">
    <thead class="text-lg border-b-2">
      <tr class="">
        <th class="font-bold">Id</th>
        <th class="font-bold">Nombre</th>
        <th class="font-bold">Edad</th>
        <th class="font-bold">Email</th>
      </tr>
    </thead>

    <tbody class="text-center">
      <tr :key="user.id" v-for="user in userList">
        <td>{{ user.id }}</td>
        <td>
          <div class="flex items-center justify-start w-52 p-3 bg-transparent">
            <img class="rounded-full w-14 ml-5 mr-2" :src="user.avatar" alt="user avatar">
            <span class="text-left">{{ `${user.first_name} ${user.last_name}` }}</span>
          </div>
        </td>
        <td>{{ userAge(user) }}</td>
        <td>{{ user.email }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    userList: Array,
  },
  methods: {
    getRandomAge(min = 18, max = 70) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
    userAge(user) {
      if (!user.birth_date) return this.getRandomAge();

      const ageDifMs = Date.now() - new Date(user.birth_date).getTime();
      const ageDate = new Date(ageDifMs);
      return Math.abs(ageDate.getUTCFullYear() - 1970);
    }
  },
  mounted() {},
};
</script>

<style>
table tbody tr:nth-child(2n) {
  background: var(--background);
}

table thead tr th {
  padding: 0 8px;
}

table tbody tr td {
  padding: 0 8px;
}
</style>

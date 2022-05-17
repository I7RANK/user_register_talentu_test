<template>
  <main class="my-5 px-3 lg:grid lg:grid-cols-3 gap-8">
    <div class="mb-5 rounded-2xl shadow-md py-5 max-w-md m-auto">
      <UserForm @userListUpdated="this.userListUpdated()"/>
    </div>

    <div class="table-content lg:col-span-2 mb-5 rounded-2xl shadow-md py-5 overflow-auto">
      <UserTable :userList="userList" v-if="responseStatus === 200"/>
    </div>
  </main>
</template>

<script>
import UserTable from './UserTable.vue'
import UserForm from './UserForm.vue'

export default {
  data() {
    return {
      userData: { data: [] },
      userList: [],
      responseStatus: 0,
    };
  },
  components: {
    UserTable,
    UserForm,
  },
  methods: {
    async getUsers() {
      const url = 'https://reqres.in/api/users?page=1';

      try {
        const res = await fetch(url);
        this.userData = await res.json();
        this.userList = this.userData.data;
        this.responseStatus = res.status;

        localStorage.setItem('userList', JSON.stringify(this.userList));
      } catch (error) {
        console.log('Error! Could not reach the API. ' + error);
      }
    },
    userListUpdated() {
      this.userList = JSON.parse(localStorage.getItem('userList'));
    }
  },
  mounted() {
    this.getUsers();
  },
};
</script>

<style>
main div {
  background: var(--background-secondary);
}
</style>
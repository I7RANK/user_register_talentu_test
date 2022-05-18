<template>
  <main class="my-5 px-3 lg:grid lg:grid-cols-3 gap-8">
    <div class="mb-5 rounded-2xl shadow-md py-5 max-w-md mx-auto self-start">
      <UserForm @userListUpdated="this.userListUpdated()"/>
    </div>

    <div class="table-content lg:col-span-2 mb-5 rounded-2xl shadow-md p-5 overflow-auto relative">
      <Spinner v-if="!responseStatus"/>
      <UserTable :userList="userList" v-if="responseStatus === 200"/>

      <div class="pagination-content w-full">
        <ul class="flex justify-center">
          <li class="mx-2 cursor-pointer" @click="currentPage > 1 ? currentPage-- : true">
            {{ '<' }}
          </li>
          <li class="mx-1 cursor-pointer" @click="this.currentPage = numberPage"
            :key="numberPage" v-for="numberPage in userData.total_pages">
            <span v-if="numberPage === currentPage" class="current-page">{{ numberPage }}</span>
            <span v-else>{{ numberPage }}</span>
          </li>
          <li class="mx-2 cursor-pointer" @click="currentPage < userData.total_pages ? currentPage++ : true">
            {{ '>' }}
          </li>
        </ul>
      </div>
    </div>
  </main>
</template>

<script>
import UserTable from './UserTable.vue'
import UserForm from './UserForm.vue'
import Spinner from './Spinner.vue'

export default {
  data() {
    return {
      userData: { data: [] },
      userList: [],
      responseStatus: 0,
      currentPage: 1,
    };
  },
  components: {
    UserTable,
    UserForm,
    Spinner,
  },
  watch: {
    currentPage() {
      this.getUsers(this.currentPage);
    }
  },
  methods: {
    async getUsers(page=1) {
      const url = `https://reqres.in/api/users?page=${page}`;

      this.responseStatus = 0;

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
    },
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

.current-page {
  text-shadow: 1px 1px 1px var(--input-color-2);
  color: var(--input-color-2);
}
</style>
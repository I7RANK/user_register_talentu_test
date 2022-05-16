<template>
  <form class="user-form flex flex-col items-center px-8" action="">
    <h2 class="text-3xl my-5">Add new user</h2>

    <div class="flex flex-col my-2">
      <label for="email">Email</label>
      <input id="email" type="text">
    </div>

    <div class="flex flex-col my-2">
      <label for="first-name">First name</label>
      <input id="first-name" type="text">
    </div>

    <div class="flex flex-col my-2">
      <label for="last-name">Last name</label>
      <input id="last-name" type="text">
    </div>

    <div class="flex flex-col my-2">
      <label for="birth-date">Birth date</label>
      <input id="birth-date" type="text">
    </div>

    <div>
    </div>
  </form>
</template>

<script>
export default {};
</script>

<style>
.user-form label {
  font-size: .8rem;
  padding: 0 1rem;
}

.user-form input {
  max-width: 212px;
  padding: 0 1rem;
  font-size: 1.2rem;
  outline: none;
  border-radius: 9999px;
  border: var(--input-color) 2px solid;
  transition: border .3s;
}

.user-form input:focus {
  border: var(--input-color-2) 2px solid;
}
</style>
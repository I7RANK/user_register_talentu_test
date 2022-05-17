<template>
  <div class="alert-content absolute right-0 z-10 py-5 px-2 rounded-lg shadow-md flex justify-between items-center">
    <p class="text-center max-w-full w-3/4 text-slate-100">{{ msg }}</p>
  </div>
</template>

<script>
export default {
  props: {
    msg: String,
  }
}
</script>

<style>
.alert-content {
  background: var(--bg-talentu);
  animation: fade-out .5s linear;
  animation-delay: 3s;
}

@keyframes fade-out {
  from {opacity: 100%;}
  to {opacity: 0%;}
}

</style>
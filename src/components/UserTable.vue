<template>
  <table class="table-auto min-w-full">
    <thead class="shadow-md text-lg">
      <tr>
        <th class="font-bold">Id</th>
        <th class="font-bold">Nombre</th>
        <th class="font-bold">Edad</th>
        <th class="font-bold">Email</th>
      </tr>
    </thead>

    <tbody class="text-center">
      <tr>
        <td>1</td>
        <td>Malcolm Lockyer</td>
        <td>1961</td>
        <td>Criminal</td>
      </tr>
      <tr>
        <td>2</td>
        <td>The Eagles</td>
        <td>1972</td>
        <td>Criminal</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {};
</script>

<style>
table tbody tr:nth-child(2n) {
  background: #eee;
}
</style>

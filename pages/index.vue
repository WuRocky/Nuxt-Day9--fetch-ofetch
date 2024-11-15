<script setup>
// // 改法一.用 useFetch
// const { data } = await useFetch("https://randomuser.me/api/");
// const [result] = data.value.results;

// // 改法二.用 useFetch 搭配 $fetch()
// const { data } = await useAsyncData("getRandomuser", () =>
//   $fetch("https://randomuser.me/api/")
// );


// // 適合使用 $fetch 的情境
// const userData = ref({});

// const getUserData = async () => {
//   const response = await $fetch("https://randomuser.me/api/");
//   userData.value = response.results[0];
// };


navigateTo("/register");
</script>

<template>
  <!-- <div>Page: index</div>

  <img
    :src="result.picture?.large"
    :alt="`${result.name.first} ${result.name?.last}`"
  />
  <h1>{{ result.name?.first }} {{ result.name?.last }}</h1>
  <h3>Email: {{ result.email }}</h3>

  <template v-if="userData.name">
    <img
      :src="userData.picture?.large"
      :alt="`${userData.name?.first} ${userData.name?.last}`"
    />
    <h1>{{ userData.name?.first }} {{ userData.name?.last }}</h1>
    <h3>Email: {{ userData.email }}</h3>
  </template>

  <button type="button" @click="getUserData">取得 User 資料</button> -->


  <div>Page: index</div>
</template>
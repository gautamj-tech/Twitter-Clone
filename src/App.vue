<template>
  <div id="app">
    <router-view :profileData="profileData" />
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      profileData: {},
    };
  },
  async created() {
     const details = await JSON.parse(localStorage.getItem('userDetails'));
    this.profileData = details[0];
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
* {
  scrollbar-width: thin;
  scrollbar-color: #aab8c2 transparent;
}

*::-webkit-scrollbar {
  width: 5px;
}

*::-webkit-scrollbar-track {
  background: transparent;
}

*::-webkit-scrollbar-thumb {
  background-color: #aab8c2;
  border-radius: 20px;
  border: transparent;
}
</style>

<template>
  <div id="app">
    <MyMain />
  </div>
</template>

<script>
import MyMain from "./components/MyMain.vue";

export default {
  name: "App",
  components: {
    MyMain,
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

img {
  display: block;
  width: 100%;
  height: 100%;
  user-select: none;
  -webkit-user-drag: none;
}

ul {
  list-style: none;
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 14px;
  color: #f5f5f5;
  background: #141414;
}

::-webkit-scrollbar {
  width: 8px;
  background: #222;
}

::-webkit-scrollbar-thumb {
  background: #d81f26;
}
</style>

<template>
  <div id="app">
    <div id="content">
      <router-view></router-view>
    </div>

  </div>
</template>
<script>

export default {
  name: "App",
  created() {
  }
};
</script>
<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  height: 100%;
  font-family: "SF Display";
}

#app {
  text-align: center;
  color: #2c3e50;
  height: 100%;
}

#content {
  height: 100%;
}

h2 {
  font-size: $fs-md;
  font-weight: bold;
  margin-bottom: 30px;
  line-height: 1.2em;
}
</style>

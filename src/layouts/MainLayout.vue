<template>
  <main class="main">
    <div class="content">
      <slot></slot>
    </div>
    <Nav/>
    <slot name="popup"/>
  </main>
</template>

<script>
import Nav from "@/components/Nav";
export default {
  name: "MainLayout",
  components: {
    Nav
  }
};
</script>

<style lang="scss">
.main {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  //height: 100%;
  background-color: #fcfcfc;
  background-image: url(../assets/images/main-bg.png);
  background-repeat: repeat-y;
  background-position: left 200px;
  background-size: 100% auto;
  min-height: 100%;
}
.content {
  flex-grow: 1;
  width: 100%;
}
.section {
  padding: 10px;
}
</style>
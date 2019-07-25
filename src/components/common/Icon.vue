<template>
  <div class="ts-icon">
    <img
      v-if="icon === 'email'"
      :src="require(`../../assets/icons/icon_email.${getExtension}`)"
      alt
    >
    <img
      v-else-if="icon === 'lock'"
      :src="require(`../../assets/icons/icon_lock.${getExtension}`)"
      alt
    >
    <img
      v-else-if="icon === 'eye'"
      :src="require(`../../assets/icons/icon_eye.${getExtension}`)"
      alt
    >
    <img
      v-else-if="icon === 'close'"
      :src="require(`../../assets/icons/icon_close.${getExtension}`)"
      alt
    >
  </div>
</template>

<script>
export default {
  props: {
    icon: {
      default: "",
      required: true
    },
    notSvg: {
      default: false
    }
  },
  computed: {
    getExtension() {
      return this.notSvg ? "png" : "svg";
    }
  }
};
</script>

<style>
</style>

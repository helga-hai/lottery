<template>
  <div class="close" @click="onClickWrapper">
    <Icon icon="close"/>
  </div>
</template>

<script>
import Icon from "@common/Icon";
export default {
  name: "CloseAction",
  components: {
    Icon
  },
  props: {
    onClick: {
      type: Function,
      default: () => {}
    }
  },
  methods: {
    onClickWrapper(event) {
      event.preventDefault();
      this.onClick(event);
    }
  }
};
</script>

<style lang="scss" scoped>
.close {
  width: 22px;
  height: 22px;
}
</style>

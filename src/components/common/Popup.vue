<template>
  <div class="popup" v-if="visible">
    <div class="popup__bg" @click="onClose"></div>
    <div class="popup__content">
      <CloseAction :onClick="onClose"/>
      <slot/>
    </div>
  </div>
</template>

<script>
import CloseAction from "@common/CloseAction";
export default {
  name: "Popup",
  components: { CloseAction },
  props: {
    visible: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    onClose(){
      this.$emit('onClose');
    }
  }
};
</script>

<style lang="scss">
.popup {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;

  &__bg {
    position: absolute;

    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.74);
  }

  &__title {
    font-size: $fs_mm;
    color: $tone-grey;
    text-align: left;
  }

  &__content {
    width: 100%;
    min-height: 420px;
    margin: 0 18px;
    border-radius: 2px;
    padding: 50px;
    background-color: #fff;
    z-index: 2;
    position: relative;
  }

  .close {
    position: absolute;
    top: 27px;
    right: 19px;
    cursor: pointer;
  }
}
</style>

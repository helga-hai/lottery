<template>
  <button :class="['btn', view]" :disabled="disabled" @click="onClick">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "TButton",
  props: {
    view: {
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    },
    text: String,
    imgURL: String,
    onClick: {
      type: Function,
      default: () => {
        console.log("click");
      }
    }
  },
  data() {
    return {};
  }
};
</script>

<style lang="scss">
.btn {
  background-color: $tone-green;
  padding: 12px 24px;
  height: 50px;
  color: $color_white;
  line-height: 24px;
  font-size: $fs_md;
  font-weight: bold;
  letter-spacing: 0.4px;
  border: 0;
  min-width: 200px;
  max-width: 324px;
  cursor: pointer;
  outline: none;
  border-radius: 29px;
  user-select: none;

  &:disabled {
    filter: grayscale(100%);
  }

  &.social {
    background-color: transparent;
    border: 1px solid $tone-social;
    color: $tone-social;
  }

  &.additional {
    border: 0;
    color: $tone-grey;
    background-color: transparent;
  }

  &.cancel {
    background-color: $tone-red;
  }

  &.fluid {
    width: 100%;
    margin: 0 auto;
  }

  &.inline {
    display: inline-block;
    width: min-content;
    min-width: min-content;
    padding: 0 12px;
  }
}
</style>

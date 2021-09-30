<template>
  <button class="buttonStyle" @click="$emit(`${text.toLowerCase() + action}`)">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    action: String,
  },
};
</script>

<style scoped>
.buttonStyle {
  background-color: #324376;
  color: #96e6b3;
  border: none;
  cursor: pointer;
  width: 100px;
  height: 25px;
}
</style>

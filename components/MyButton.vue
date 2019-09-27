<template>
  <div :class="theme[type]">
    <slot/>
  </div>
</template>

<script>
export default {
  name: "MyButton",
  inject: {
    theme: {
      from: "theme",
      default() {
        return this.defaultTheme;
      }
    }
  },
  props: ["type"]
};
</script>

<style module="defaultTheme">
.primary {
  background: blue;
  color: white;
}
</style>
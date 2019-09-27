<template>
  <div id="app">
    <h2>Static template:</h2>
    <Button>Hello</Button>
    <MyButton type="primary">Hello</MyButton>
    <MyButton type="secondary">Hello</MyButton>

    <h2>Dynamically inserted:</h2>
    <div ref="container">
      <button @click="onClick">Click to insert MyButtons</button>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import MyButton from "./components/MyButton";

export default {
  name: "app",
  components: { MyButton },
  provide() {
    return {
      theme: this.theme
    };
  },
  methods: {
    onClick() {
      var ComponentClass = Vue.extend(MyButton);
      var instance = new ComponentClass({
        propsData: { type: "primary" },
        parent: this
      });
      instance.$slots.default = [<b>"Klikni me!"</b>];
      instance.$mount(); // pass nothing
      this.$refs.container.appendChild(instance.$el);
    }
  },
  hello: function(e) {
    console.log("I was clicked!");
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<style module="theme">
.primary {
  /* now everybody likes green ;) */
  background-color: green;
  padding-top: 5px;
  padding-bottom: 5px;
  border: 1px solid white;
  /* and css-colors! */
  color: white;
}
.secondary {
  /* now everybody likes green ;) */
  background-color: red;
  /* and css-colors! */
  color: white;
}
</style>
<template>
  <div id="app">
    <button class="button" id="show-modal" @click="showModal = true">
      Show Modal
    </button>
    <ModalWindow
      v-show="showModal"
      @close="showModal = false"
      title="Draggable Window"
    >
      <img src="./assets/img/lion.jpg" slot="body" />
    </ModalWindow>
  </div>
</template>

<script>
import ModalWindow from "./components/ModalWindow";

export default {
  name: "App",
  components: {
    ModalWindow,
  },

  data() {
    return {
      showModal: false,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.button {
  display: inline-block;

  color: #ffffff;
  font-style: normal;
  overflow: hidden;
  text-align: center;
  text-decoration: none;
  text-overflow: ellipsis;
  font-family: inherit;
  white-space: nowrap;
  font-weight: 700;
  padding: 19px 39px 18px;
  font-size: 28px;

  border-style: solid;
  border-radius: 6px;
  border-width: 0px 0px 3px;
  box-shadow: 0 -1px 0 rgba(255, 255, 255, 0.1) inset;
  background-color: #e2525c;

  cursor: pointer;
  transition: all 200ms ease-in-out 0s;
}

.button:hover,
.button:focus {
  color: rgba(255, 255, 255, 0.7);
}

.button:active {
  opacity: 0.7;
}
</style>

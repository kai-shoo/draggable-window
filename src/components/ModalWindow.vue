<template>
  <transition name="modal">
    <div class="modal-mask" @mouseup="stopDrag" @mousemove.prevent="doDrag">
      <div
        class="modal-container"
        :style="style"
        @mousedown.prevent="startDrag"
      >
        <div class="modal-header">
          <h3>{{ title }}</h3>
          <button class="modal-close-button" @click="$emit('close')"></button>
        </div>
        <div class="modal-body">
          <slot name="body"> </slot>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ModalWindow",
  props: {
    title: String,
  },

  data: function () {
    return {
      dragging: false,
      left: 0,
      top: 0,
      mouseLeft: 0,
      mouseTop: 0,
    };
  },
  methods: {
    startDrag: function (event) {
      this.dragging = true;
      this.startX = event.clientX;
      this.startY = event.clientY;
    },

    doDrag: function (event) {
      if (this.dragging) {
        this.mouseLeft = event.clientX - this.startX;
        this.mouseTop = event.clientY - this.startY;
      }
    },
    stopDrag() {
      if (this.dragging) {
        this.dragging = false;

        this.top += this.mouseTop;
        this.left += this.mouseLeft;
        this.mouseLeft = 0;
        this.mouseTop = 0;
      }
    },
  },
  computed: {
    style() {
      return {
        transform: `translate(${this.left + this.mouseLeft}px, ${
          this.top + this.mouseTop
        }px)`,
      };
    },
  },
};
</script>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;

  display: flex;
  width: 100%;
  height: 100%;

  background-color: rgba(41, 171, 164, 0.8);
  transition: opacity 0.3s ease;
}

.modal-container {
  position: relative;

  min-width: 300px;
  min-height: 200px;
  margin: auto;
  padding: 0;

  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);

  font-family: Helvetica, Arial, sans-serif;
}

.modal-header {
  display: flex;
  height: 60px;
  padding: 12px 30px;
  align-items: center;
  justify-content: flex-end;

  overflow: hidden;
  background: #e2525c;
}

.modal-header h3 {
  flex-grow: 1;
  margin: 0;

  color: white;
  font-size: 40px;
  text-align: left;
  margin-right: 40px;

  pointer-events: none;
}

.modal-body {
  margin: 20px 0;
}

.modal-body >>> img {
  display: block;
  max-height: 400px;
  object-fit: cover;
  margin-left: auto;
  margin-right: auto;

  pointer-events: none;
}

.modal-close-button {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 40px;
  overflow: hidden;

  cursor: pointer;

  background-color: transparent;
  border: none;
  appearance: none;
}

.modal-close-button::after,
.modal-close-button::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 0;

  height: 12px;
  margin-top: -6px;
  width: 100%;

  border-radius: 5px;
  transform: rotate(45deg);
  background: white;
}

.modal-close-button::after {
  transform: rotate(-45deg);
}

.modal-close-button::after {
  transform: rotate(-45deg);
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>

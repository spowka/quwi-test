<template>
  <div class="modalContainer">
    <div class="bg" @click="close"></div>
    <div class="modal">
      <button class="close" @click="close">X</button>
      <input type="text" placeholder="NAME" v-model="newName" />
      <button @click="save">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return { newValue: "" };
  },
  computed: {
    newName: {
      get() {
        return this.name;
      },
      set(newValue) {
        return (this.newValue = newValue);
      },
    },
  },
  props: {
    name: "",
  },
  methods: {
    save() {
      console.log(this.newValue);
      this.$emit("save", this.newValue);
    },
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.modalContainer {
  width: 100%;
  height: calc(100vh - 45px);
  position: absolute;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
.bg {
  width: 100%;
  height: calc(100vh - 45px);
  position: absolute;
  background: rgba(0, 0, 0, 0.418);
}
.modal {
  width: 440px;
  padding: 45px 40px 25px;
  background: #fff;
  text-align: center;
  box-shadow: 0 0 12px rgb(0 0 0 / 25%);
  border-radius: 15px;
  position: relative;
}
.modal input {
  width: 100%;
  height: 48px;
  padding: 15px;
  outline: none;
  border: 1px solid #dadada;
  border-radius: 5px;
  margin-bottom: 15px;
}
.modal button {
  width: 100%;
  height: 48px;
  border: none;
  border-radius: 5px;
  background: #2668c1;
  color: #fff;
  font-size: 18px;
  margin: 10px 0 15px;
  cursor: pointer;
}
.modal .close {
  position: absolute;
  right: 25px;
  top: 5px;
  padding: 0;
  background: none;
  color: black;
  height: auto;
  width: auto;
}
</style>

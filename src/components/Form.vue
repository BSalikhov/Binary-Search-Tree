<template>
  <div class="form">
    <input v-model="value" type="number" />
    <button class="add-btn" @click="add">Add</button>
    <button class="delete-btn" @click="remove">Delete</button>
  </div>
</template>

<script>
export default {
  name: "Form",

  data: () => ({
    value: null,
  }),

  methods: {
    add() {
      this.$emit("add", this.value);
      this.value = null;
    },

    remove() {
      this.$emit("remove", this.value);
      this.value = null;
    },
  },
};
</script>

<style>
.form {
  margin-top: 50px;
}

button {
  border: none;
  padding: 12px 20px;
  color: white;
  font-size: 18px;
  font-weight: 600;
  border-radius: 6px;
  margin-left: 8px;
  cursor: pointer;
}

input {
  height: 46px;
  box-sizing: border-box;
  padding: 0 8px;
  font-size: 18px;
  border-radius: 6px;
  border-style: solid;
}

.add-btn {
  background: #22c55e;
}

.delete-btn {
  background: #ef4444;
}
</style>

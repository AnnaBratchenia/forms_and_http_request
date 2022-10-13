<template>
  <h3>Can you estimate your knowledge?</h3>
  <ul>
    <li><button class="btn" @click="defineRating('poor')">Poor</button></li>
    <li>
      <button class="btn" @click="defineRating('average')">Average</button>
    </li>
    <li><button class="btn" @click="defineRating('great')">Great</button></li>
  </ul>
</template>

<script>
export default {
  props: ["modelValue"],
  emits: ["update:modelValue"],
  methods: {
    defineRating(option) {
      this.$emit("update:modelValue", option);
      console.log(option);
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.btn {
  border: none;
  background-color: rgba(30, 201, 141, 0.158);
  padding: 1.5rem 3.5rem;
}
.btn:hover {
  background-color: rgb(176, 129, 197);
  font-weight: bold;
}
</style>

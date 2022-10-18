<template>
  <ul class="personsl-card">
    <li>
      <p>
        Name: <span class="common-style">{{ name }}</span>
      </p>
      <p>
        Age: <span class="common-style"> {{ age }}</span>
      </p>
      <p>
        How do you learn? <span class="common-style"> {{ how }}</span>
      </p>
      <p>
        What are you interested in?
        <span class="common-style"> {{ interest.join(", ") }}</span>
      </p>
      <p>
        How did you hear about us?
        <span class="common-style"> {{ referer }}</span>
      </p>
      <p>
        Estimate knowledge:
        <span
          v-bind:class="{
            poor: this.rating === 'poor',
            average: this.rating === 'average',
            great: this.rating === 'great',
          }"
          class="rating-style"
          >{{ rating }}</span
        >
      </p>
      <base-button @click="deleteInfo(id)">Delete</base-button>
    </li>
  </ul>
</template>
<script>
export default {
  props: ["name", "id", "age", "how", "interest", "referer", "rating"],
  emits: ["deletedItem"],
  data() {
    return {
      // ratingInfo= this.rating,
    };
  },
  methods: {
    deleteInfo(id) {
      this.$emit("deletedItem", id);
    },
  },
};
</script>
<style scoped>
.personsl-card {
  border: 1px solid #b8b6b6;
  box-shadow: 5px 5px 30px #b8b6b6;
  list-style: none;
}
.common-style {
  text-transform: capitalize;
  font-size: 30px;
}
.rating-style {
  padding-left: 15px;
  padding-right: 15px;
  border-radius: 10px;
  color: white;
}
.poor {
  background-color: brown;
}
.average {
  background-color: blue;
}
.great {
  background-color: green;
}
</style>

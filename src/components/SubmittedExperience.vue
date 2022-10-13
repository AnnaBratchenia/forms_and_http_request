<template>
  <base-card>
    <h2>Submitted Experiences</h2>
    <base-button @click="loadExperiences"
      >Load Submitted Experiences</base-button
    >
    <ul>
      <li v-for="res in experiencesResult" v-bind:key="res.id">
        <p>{{ res.name }}</p>
        <p>{{ res.age }}</p>
        <p>{{ res.how }}</p>
        <p>{{ res.referer }}</p>
        <p>{{ res.rating }}</p>
      </li>
    </ul>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      experiencesResult: [],
    };
  },
  methods: {
    loadExperiences() {
      fetch("https://vue-project-c8624-default-rtdb.firebaseio.com/survey.json")
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) => {
          const result = [];
          for (const id in data) {
            result.push({
              id: id,
              name: data[id].name,
              age: data[id].age,
              how: data[id].how,
              referer: data[id].referer,
              rating: data[id].rating,
            });
          }
          this.experiencesResult = result;
          console.log(this.experiencesResult);
        });
    },
  },
};
</script>

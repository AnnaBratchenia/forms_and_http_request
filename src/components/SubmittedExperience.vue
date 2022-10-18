<template>
  <base-card>
    <h2>Submitted Experiences</h2>
    <base-button @click="loadExperiences"
      >Load Submitted Experiences</base-button
    >
    <div v-if="buttonClicked">
      <add-experience
        v-for="exp in experiencesResult"
        v-bind:key="exp.id"
        v-bind:id="exp.id"
        v-bind:name="exp.name"
        v-bind:age="exp.age"
        v-bind:interest="exp.interest"
        v-bind:how="exp.how"
        v-bind:referer="exp.referer"
        v-bind:rating="exp.rating"
        @deletedItem="deletePersonalInfo"
      ></add-experience>
    </div>

    <!-- <ul>
      <li v-for="res in experiencesResult" v-bind:key="res.id">
        <p>{{ res.name }}</p>
        <p>{{ res.age }}</p>
        <p>{{ res.how }}</p>
        <p>{{ res.referer }}</p>
        <p>{{ res.rating }}</p>
      </li>
    </ul> -->
  </base-card>
</template>

<script>
import AddExperience from "./AddExperiences.vue";

export default {
  components: { AddExperience },
  data() {
    return {
      experiencesResult: [],
      buttonClicked: false,
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
              interest: data[id].interest,
              referer: data[id].referer,
              rating: data[id].rating,
            });
          }
          this.experiencesResult = result;
          console.log(this.experiencesResult);
        });
      this.buttonClicked = true;
    },
    deletePersonalInfo(idPerson) {
      fetch(
        `https://vue-project-c8624-default-rtdb.firebaseio.com/survey/${idPerson}.json`,
        { method: "DELETE" }
      ).then(() => {
        this.experiencesResult = this.experiencesResult.filter(
          (itemId) => itemId.id !== idPerson
        );
      });
      console.log(`Deleted ${idPerson}`);
    },
  },
};
</script>

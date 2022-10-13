<template>
  <base-card>
    <div
      class="form-control"
      v-bind:class="{ invalid: userNameValidity === 'invalid' }"
    >
      <label for="user-name">Your name</label>
      <input
        id="user-name"
        name="user-name"
        type="text"
        v-model="userName"
        @blur="emptyField"
      />
      <p v-if="userNameValidity === 'invalid'">Please enter a valid name</p>
    </div>
    <div class="form-control">
      <label for="age">Your age</label>
      <input id="age" name="age" type="number" v-model="userAge" />
    </div>
    <div class="form-control">
      <label for="referer">How did you hear about us?</label>
      <select name="referer" v-model="referer">
        <option value="google">Google</option>
        <option value="yandex">Yandex</option>
        <option value="radio">Radio</option>
      </select>
    </div>
    <div class="form-cotrol">
      <h3>What are you interested in?</h3>
      <div>
        <input
          id="interest-news"
          name="interest"
          value="news"
          type="checkbox"
          v-model="interest"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          id="interest-tutorials"
          name="interest"
          value="tutorials"
          type="checkbox"
          v-model="interest"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          id="interest-nothing"
          name="interest"
          value="nothing"
          type="checkbox"
          v-model="interest"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h3>How do you learn?</h3>
      <div>
        <input
          id="video"
          name="video"
          value="video"
          type="radio"
          v-model="how"
        />
        <label for="video">Video Courses</label>
      </div>
      <div>
        <input id="blog" name="blog" value="blog" type="radio" v-model="how" />
        <label for="blog">Blogs</label>
      </div>
      <div>
        <input
          id="other"
          name="other"
          value="other"
          type="radio"
          v-model="how"
        />
        <label for="other">Other</label>
      </div>
    </div>
    <rating-control v-model="rating"></rating-control>

    <base-button @click="saveForm">Save Data</base-button>
  </base-card>
</template>
>

<script>
import BaseCard from "./UI/BaseCard.vue";
import BaseButton from "./UI/BaseButton.vue";
import RatingControl from "./RatingControl.vue";

export default {
  components: { BaseCard, BaseButton, RatingControl },
  data() {
    return {
      userName: "",
      userAge: null,
      referer: "radio",
      interest: [],
      how: "",
      userNameValidity: "pending",
      rating: null,
    };
  },
  methods: {
    saveForm() {
      fetch(
        "https://vue-project-c8624-default-rtdb.firebaseio.com/survey.json",
        {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            name: this.userName,
            age: this.userAge,
            referer: this.referer,
            interest: this.interest,
            how: this.how,
            rating: this.rating,
          }),
        }
      );
      console.log(this.userName);
      console.log(this.userAge);
      console.log(this.referer);
      console.log(this.interest);
      console.log(this.how);
      console.log(this.rating);
    },
    emptyField() {
      if (this.userName === "") {
        this.userNameValidity = "invalid";
      } else {
        this.userNameValidity = "valid";
      }
    },
  },
};
</script>

<style scoped>
label {
  margin-bottom: 1rem;
}
.form-control {
  font-size: 20px;
  margin-bottom: 1.5rem;
  display: flex;
  flex-direction: column;
}
.checkbox-control {
  display: flex;
}
.invalid {
  color: red;
}
.invalid input {
  border-color: red;
}
</style>

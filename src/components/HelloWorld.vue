<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div v-if="displayName && firstName">WELCOME {{ displayName }}</div>
    <div v-if="displayName && lastName">
      WELCOME {{ isMale ? "MR" : "MS" }} {{ displayName }}
    </div>
    <div>
      <input type="checkbox" id="checkbox" v-model="isMale" />
      <label for="checkbox">Are you Male??</label>
    </div>
    <template v-if="isInputFirstName">
      <label>First Name</label>
      <input
        v-model="firstName"
        placeholder="Enter your first name"
        key="firstname"
      />
    </template>
    <template v-else>
      <label>Last Name</label>
      <input
        v-model="lastName"
        placeholder="Enter your last name"
        key="lastname"
      />
    </template>
    <button v-on:click="getBookRecomendations()">
      Get your book reconmendation
    </button>
    <button v-on:click="isInputFirstName = !isInputFirstName">
      Toggle input field
    </button>
    <template v-if="bookRecomendations.length !== 0">
      <Book
        :title="bookRecomendations[0].title"
        :author="bookRecomendations[0].author"
      />
    </template>
  </div>
</template>

<script>
import Book from "./Book";
export default {
  name: "HelloWorld",
  components: { Book },
  props: {
    msg: String,
  },
  data: () => {
    return {
      firstName: "",
      lastName: "",
      isInputFirstName: true,
      isMale: true,
      bookRecomendations: [],
    };
  },
  computed: {
    displayName: function() {
      if (this.firstName) {
        return this.firstName.toUpperCase();
      } else if (this.lastName) {
        return this.lastName.toUpperCase();
      } else return "";
    },
  },
  methods: {
    getBookRecomendations: async function() {
      if (!this.firstName && !this.lastName) {
        alert(
          "Tell us your first name or last name before we recomend a book!"
        );
        return;
      }
      try {
        const res = await fetch("https://fakerapi.it/api/v1/books?_quantity=1");
        const data = await res.json();
        console.log(data.data);
        this.bookRecomendations = data.data;
      } catch (error) {
        alert(error.message);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

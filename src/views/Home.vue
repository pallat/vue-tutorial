<template>
  <div class="home">
    {{ 1 + 1}}
    {{ name }}
    <input :placeholder="placeholderName" type="text" v-model="name" />
    <ul>
      <li v-for="(book, index) in books" :key="index">{{ book.name }} score {{ book.score }}</li>
    </ul>

    <div v-show="toggle">Hello {{ name }}</div>
    <div v-if="!toggle">Good morning</div>
    <button v-on:click="clickToggle">Toggle</button>

    <br />

    <form class="container" @submit.prevent="createABook">
      <div class="form-group row">
        <label for="name">Title</label>
        <input id="name" class="form-control" type="text" v-model="title" />
      </div>

      <div class="form-group row">
        <label for="score">Score</label>
        <select class="form-control" name="score" id="score">
          <option v-for="(s, index) in 10" value="s" :key="index">{{ s }}</option>
        </select>
      </div>
      <input type="submit" class="btn btn-primary" />
    </form>

    <form @submit.prevent="fetchReviews">
      <input type="submit" class="btn btn-primary" />
    </form>

    <br />
    {{ highScoreBooks }}
    <br />
    {{ totalHighScoreBooks() }}
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "home",
  components: {},
  methods: {
    clickToggle() {
      this.toggle = !this.toggle;
    },
    totalHighScoreBooks() {
      return this.books.filter(b => b.score > 6).length;
    },
    createABook() {
      const book = { name: this.title, score: this.score };
      this.books.push(book);
    },
    fetchReviews() {
      this.axios.get("http://localhost:3000/reviews").then(response => {
        console.log(response.data);
      });
    }
  },
  computed: {
    highScoreBooks() {
      return this.books.filter(b => b.score > 6);
    }
  },
  data() {
    return {
      name: "John",
      placeholderName: "input your name",
      title: "",
      score: 0,
      books: [
        { name: "Harry Potter", score: 9 },
        { name: "Percy Jackson", score: 7 },
        { name: "How to train the dragon", score: 5 }
      ],
      toggle: true
    };
  }
};
</script>

<style lang="css" scoped></style>

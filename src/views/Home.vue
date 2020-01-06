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

    <form @submit.prevent="createABook">
      <input type="text" v-model="title" />
      <input type="text" v-model="score" />
      <input type="submit" />
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

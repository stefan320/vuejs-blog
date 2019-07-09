<template>
  <div class="blogs">
    <div class="side-hero"></div>
    <!-- <img class="side-hero" src="./assets/blog-img.jpg" /> -->
    <div class="section--container">
      <div class="section-div">
        <h1 class="section-title">Latest Posts</h1>
        <div class="select-div">
          <select class="select" v-model="searchCategory">
            <option value>Category</option>
            <option value="mobile">Mobile</option>
            <option value="desktop">Desktop</option>
          </select>
        </div>
      </div>
    </div>

    <div class="posts">
      <article
        v-for="(article, index) in filterCategory"
        @click="summary[index].show = !summary[index].show"
        :key="article.id"
        class="article-div"
      >
        <h1 class="header">{{article.title}}</h1>
        <h2 class="header-secondary">
          Category:
          <span class="capitalize">{{article.category}}</span>
        </h2>
        <h2 class="header-secondary">
          Author:
          <span class="capitalize">{{article.author}}</span>
        </h2>
        <p class="paragraph" v-if="summary[index].show">{{articleSummary(article.text)}}</p>
        <p class="paragraph" v-else>{{article.text}}</p>
        <Comments :articleInfo="article" :index="index" :visable="summary[index]" />
      </article>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import Comments from "./Comments";
export default {
  name: "blogs",
  components: {
    Comments
  },
  data() {
    return {
      articles: [],
      searchCategory: "",
      summary: [{ show: true }, { show: true }, { show: true }]
    };
  },
  methods: {
    // 1) Remove spaces from article and add each word to summary array
    // 2) Use reduce method to add words until the limit of words is reached (IF limit of words the new next word exceed the limit the next word will not be added)
    // 3) Use join to concat back the words
    articleSummary: (article, limit = 100) => {
      const summary = [];
      if (article.length > limit) {
        article.split(" ").reduce((acc, curVal) => {
          if (acc + curVal.length < limit) {
            summary.push(curVal);
            return acc + curVal.length;
          }
        }, 0);

        return `${summary.join(" ")} ...`;
      }
      return article;
    }
  },
  computed: {
    // Returns the articles matching the selectred category
    filterCategory() {
      return this.articles.filter(article => {
        return article.category.match(this.searchCategory);
      });
    }
  },
  created() {
    const proxy = "https://cors-anywhere.herokuapp.com/";
    const data = {};
    axios
      .get(
        `${proxy}https://d2rsw2kbemic8w.cloudfront.net/items/3S2Y290c2A2M2m400Y1J/sampledata.json`
      )
      .then(response => {
        this.articles = response.data.articles;
      });
  }
};
</script>

<style>
.posts {
  display: flex;
  flex-direction: column;
  background-color: #fff;
  max-width: 120rem;
  margin: 0 auto;
}
.side-hero {
  max-width: 100%;
  height: 90vh;
  background: url("./assets/blog-img.jpg") no-repeat bottom;
  background-size: cover;
}

.section--container {
  background-color: #1e2022;
}
.section-div {
  display: flex;
  background-color: #1e2022;
  text-align: center;
  padding: 3rem;
  font-size: 2rem;
  color: #f0f5f9;
  max-width: 82rem;
  margin: 0 auto;
}
.section-title {
  margin-right: auto;
  font-size: 3rem;
}
.select-div {
  text-align: center;
  top: 3rem;
  right: 10rem;
}
.select {
  outline: transparent;
  width: 8rem;
  padding: 1rem;
  box-sizing: content-box;
  border: none;
  background-color: #f0f5f9;
  border-radius: 20px;
}

select {
  outline: transparent;
  border: none;
}
.article-div {
  padding: 3rem;
  margin: 0 auto;
  border-bottom: 1px solid #1e2022;
  cursor: pointer;
  color: #1e2022;
  max-width: 82rem;
}
.header {
  font-size: 2rem;
  padding: 0;
}

.capitalize {
  text-transform: capitalize;
}

.header-secondary,
.header-secondary > span {
  font-size: 1.4rem;
  font-weight: 400;
}

.paragraph {
  color: #1e2022;
  font-size: 1.6rem;
  font-weight: 400;
  padding: 0.7rem 0;
  display: inline-block;
}

@media only screen and (min-width: 82rem) {
  .article-div {
    padding: 3rem 0;
  }
  .side-hero {
    background-attachment: fixed;
    background-position: top;
  }
}
</style>

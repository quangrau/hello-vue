<template>
  <div class="container home">
    <h1>Hello Vue! <small>Please choose a source, and I will get the hotest feeds for you!</small></h1>
    <form @submit.prevent="search">
      <div class="home__form form-group row">
        <label for="sourceName" class="col-md-2 col-form-label">Source</label>
        <div class="col-md-6">
          <select v-model="source" class="form-control" id="sourceName">
            <option value="hackerNews">Hacker News</option>
            <option value="productHunt">Product Hunt</option>
            <option value="github">Github</option>
            <option value="medium">Medium</option>
            <option value="techCrunch">TechCrunch</option>
          </select>
        </div>
      </div>
      <div class="form-group row">
        <label for="filter" class="col-md-2 col-form-label">Filter</label>
        <div class="col-md-6">
          <select v-model="filter" class="form-control" id="filter">
            <option value="popular">Popular</option>
            <option value="latest">Latest</option>
          </select>
        </div>
      </div>
      <div class="form-group row">
        <label for="limit" class="col-md-2 col-form-label">Limit</label>
        <div class="col-md-6">
          <input v-model="limit" type="number" class="form-control" id="limit" placeholder="30">
        </div>
      </div>
      <div class="form-group row">
        <div class="offset-sm-2 col-md-10">
          <button type="submit" class="btn btn-primary">Load</button>
        </div>
      </div>
    </form>

    <div class="home__result">
      <div v-if="feeds.length">
        <ul class="feeds">
          <li class="feeds__item" v-for="(feed, index) in feeds">
            <a target="_blank" :href="feed.url.panda">
              <span class="feeds__item__num">
                {{ index + 1 }}
              </span>
              <span class="feeds__item__title">
                {{ feed.title }}
              </span>
            </a>
          </li>
        </ul>
      </div>
      <div v-else>
        <div class="alert alert-danger">
          {{ errorMsg }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(VueAxios, axios);

export default {
  name: 'home',
  data() {
    return {
      source: 'hackerNews',
      filter: 'popular',
      limit: 30,
      page: 1,
      feeds: [],
      errorMsg: '',
    };
  },

  methods: {
    search() {
      const endpoint = 'https://cdnapi.pnd.gs/v2/feeds';
      const api = `${endpoint}?limit=${this.limit}&page=${this.page}&sort=${this.filter}&sources=${this.source}`;

      Vue.axios.get(api).then((response) => {
        this.feeds = response.data;
      }).catch(() => {
        this.errorMsg = 'No user or no location!';
        this.feeds = [];
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a:hover {
  text-decoration: none;
}
.home {
  padding-top: 30px;
}
.home__form {
  padding-top: 30px;
}
.home__result {
  padding: 30px 0;
}
.home__result .feeds {
  margin: 0;
  padding: 0;
  list-style: none;
}
.home__result .feeds__item {
  padding: .5rem;
  border: 1px solid #eceef1;
  border-top-color: #FFF;
}
.home__result .feeds__item a {
  color: #2a3e52;
  display: flex;
  align-items: center;
}
.home__result .feeds__item:first-child {
  border-top-color: #eceef1;
}
.home__result .feeds__item__num {
  width: 30px;
  height: 30px;
  line-height: 30px;
  border-radius: 2;
  background-color: #ff6500;
  color: #FFF;
  text-align: center;
  font-size: 18px;
}
.home__result .feeds__item__title {
  padding-left: .5rem;
  font-weight: 500;
}
</style>

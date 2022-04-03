<template>
  <div class="container">
    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
      <div class="input-group mx-sm-3 mb-2">
        <label class="visually-hidden" for="search">Search</label>
        <input
          type="search"
          name="search"
          v-model="searchTerm"
          id="search"
          class="form-control mb-2 mr-sm-2"
          placeholder="Enter search term here"
        />
        <button class="btn btn-primary mb-2">Search</button>
      </div>
      <p>You are searching for {{ searchTerm }}</p>
    </form>

    <div class="w-100 row container justify-content-center">
      <div class="py-4 col-md-4 col-sm-6" v-for="article in articles">
        <div class="card h-100">
          <img :src="article.urlToImage" :alt="article.title" />
          <div class="card-image"></div>
          <div class="card-body">
            <h6>{{ article.title }}</h6>
            <small class="text-muted">{{
              `Source ${article.source.name}`
            }}</small>

            <p class="mt-4">{{ article.description }}</p>
            <small class="text-muted">{{
              `Published ${new Date(article.publishedAt).toString()}`
            }}</small>
          </div>

          <div class="card-footer">
            <a :href="article.url" class="btn btn-primary w-100">Learn More</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      articles: [],
      searchTerm: "",
    };
  },

  methods: {
    searchNews() {
      let self = this;
      fetch(
        `https://newsapi.org/v2/everything?q=${self.searchTerm}&language=en`,
        {
          headers: {
            Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
          },
        }
      ).then(async (response) => {
        const { articles } = await response
          .json()
          .catch((error) => console.log(error));

          self.articles = articles ? articles : []
      });
    },
  },

  created() {
    const self = this;
    fetch("https://newsapi.org/v2/top-headlines?country=us", {
      headers: {
        Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
      },
    })
      .then(async (response) => {
        const { articles } = await response
          .json()
          .catch((error) => console.log(error));
        self.articles = articles;
      })
      .catch((error) => console.log(error));
  },
};
</script>

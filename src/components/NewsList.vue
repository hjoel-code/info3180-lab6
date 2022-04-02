<template>
  <div class="w-100 row container justify-content-center">
    <div class="py-4 col-md-4 col-sm-6" v-for="article in articles">
      <div class="card h-100">
          <img :src="article.urlToImage" :alt="article.title" />
        <div class="card-image">
          
        </div>
        <div class="card-body">
            <h6>{{article.title}}</h6>
            <small class="text-muted">{{ `Source ${article.source.name}` }}</small>
            

            <p class="mt-4">{{ article.description}}</p>
            <small class="text-muted">{{ `Published ${new Date(article.publishedAt).toString()}` }}</small>
        </div>

        <div class="card-footer">
            <a :href="article.url" class="btn btn-primary w-100">Learn More</a>
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
    };
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

        console.log(articles);
      })
      .catch((error) => console.log(error));
  },
};
</script>

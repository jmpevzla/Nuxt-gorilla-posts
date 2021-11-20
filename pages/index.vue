<template>
  <section class="container">
    <h1 class="text-center">Gorilla News Posts</h1>
    <div>
      <md-content
        class="md-layout md-gutter"
        style="background: #ccc; padding: 5px"
      >
        <ul
          v-for="post in posts"
          :key="post.id"
          class="
            md-layout-item
            md-large-size-25
            md-medium-size-33
            md-small-size-50
            md-xsmall-size-100
          "
        >
          <md-card md-with-hover style="margin-top: 10px">
            <md-card-media>
              <img
                :alt="post.title.rendered"
                v-if="post._embedded"
                :src="
                  post._embedded['wp:featuredmedia'][0].media_details.sizes
                    .medium_large.source_url
                "
              />
            </md-card-media>

            <md-card-header>
              <div class="md-title">
                <a
                  target="_blank"
                  :href="post.link"
                  :title="post.title.rendered"
                  >{{ post.title.rendered }}</a
                >
              </div>
              <div class="md-subhead" v-if="post._embedded">
                {{ post._embedded.author[0].name }}
              </div>
            </md-card-header>

            <md-card-content>
              <md-button class="md-icon-button">
                <md-icon class="small-icon">bookmark</md-icon>
              </md-button>

              <md-button class="md-icon-button">
                <md-icon class="small-icon">share</md-icon>
              </md-button>
            </md-card-content>
          </md-card>
        </ul>
      </md-content>
    </div>
  </section>
</template>

<style lang="scss">
  .text-center {
    text-align: center;
  }
</style>

<script>
export default {
  async asyncData({ app }) {
    const posts = await app.$axios.$get('/api/?_embed')
    console.log(posts)
    return { posts }
  },
}
</script>

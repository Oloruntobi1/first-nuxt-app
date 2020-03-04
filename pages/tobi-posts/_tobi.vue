<template>
<div class="container">
    <article>
        <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>
    </article>
    <aside>
      <h3>Posts you might enjoy</h3>
      <ul>
        <li v-for="related in relatedPosts" :key="related.title">
          <nuxt-link :to="{name: 'tobi-posts-tobi', params: {tobi: related.id}}">
            {{related.title}}
          </nuxt-link>
        </li>
      </ul>
    </aside>
    </div>
</template>

<script>
export default {
   head () {
      return {
        title: this.post.title,
        meta: [
          { name: 'twitter:title', content: this.post.title},
          { name: 'twitter:description', content: this.post.content},
          { name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png'},
          { name: 'twitter:card', content: 'summary_large_image'}
        ]
      }
    },
    data () {
      return {
        // the tobi had to match with the underscore whatever i had saved the file with itself
        id: this.$route.params.tobi,
        
      }
    },
    computed: {

      //returns active post
      post () {
        // return this.posts.find(post => post.id === this.id)
         return this.$store.state.posts.all.find(post => post.id === this.id)
      },
      relatedPosts () {
        // return this.posts.filter(post => post.id !== this.id)
         return this.$store.state.posts.all.filter(post => post.id !== this.id)
    }
  }

}

</script>

<style scoped>
    .container {
    display: flex;
    justify-content: space-between;
    line-height: 1.5;
  }
  article * {
    margin-bottom: 1rem;
  }
  aside {
    min-width: 280px;
    max-width: 280px;
    padding-left: 2rem;
  }
  .title {
    font-size: 2rem;
  }
</style>

<template>
  <section class="slug">
    <h1 class="slug_title">
      {{ article.fields.title }}
    </h1>
    <p class="slug_date">{{ article.sys.updatedAt }}</p>
    <div>
      {{ article.fields }}
    </div>
  </section>
</template>
<script>
import { createClient } from '~/plugins/contentful.js'

const client = createClient()
export default {
  props: {
    id: {
      type: String,
      default: ''
    }
  },
  transition: 'slide-right',
  async asyncData({ params }) {
    return await client
      .getEntry(params.sys)
      .then((entrie) => {
        console.log(entrie)
        return {
          article: entrie
        }
      })
      .catch(console.error)
  }
}
</script>

<template>
  <Layout>
    <div>
      <article v-for="post in $page.posts.edges" :key="post.id" >
        <time :datetime="post.node.date">{{ post.node.date }}</time><h2><g-link :to="post.node.path" rel="bookmark">{{ post.node.title }}</g-link></h2>
      </article>
    </div>
  </Layout>
</template>

<page-query>
query Posts ($page: Int) {
  posts: allPost (sortBy: "date", order: DESC, perPage: 10, page: $page) @paginate {
    totalCount
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        date (format: "YYYY-MM-DD")
        summary
        path
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: 'Blog'
  },
}
</script>
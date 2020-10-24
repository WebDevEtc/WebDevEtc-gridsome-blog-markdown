<template>
  <div>
    <article v-for="post in $page.posts.edges" :key="post.id" >
      <h2><g-link :to="post.node.path" rel="bookmark">{{ post.node.title }}</g-link></h2>
      <p>Posted on <time :datetime="post.node.date">{{ post.node.date }}</time></p>

      <p>{{ post.node.summary }}</p>
    </article>

    <h2>Pagination</h2>
    <Pager :info="$page.posts.pageInfo"/>
  </div>
</template>

<page-query>
query Posts ($page: Int) {
posts: allPost (sortBy: "date", order: DESC, perPage: 5, page: $page) @paginate {
totalCount
pageInfo {
totalPages
currentPage
}
edges {
node {
id
title
date (format: "MMMM D, Y")
summary
path
}
}
}
}
</page-query>

<script>
import { Pager } from 'gridsome'

export default {
  components: {
    Pager
  },
  metaInfo: {
    title: 'View my blog posts'
  },
}
</script>

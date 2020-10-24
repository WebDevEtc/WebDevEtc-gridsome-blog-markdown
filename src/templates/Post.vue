<template>
    <article>
      <h1>{{ $page.post.title }} </h1>

      <div>
        Tags:
        <g-link
            v-for="tag in $page.post.tags"
            :to="tag.path"
            :key="tag.id">
          #{{ tag.title }}
        </g-link>
      </div>

      <p>Posted on {{ $page.post.date }}</p>

      <div class="markdown-body mb-8" id="article-area" v-html="$page.post.content" />
    </article>
</template>

<page-query>
query Post ($path: String!) {
post: post (path: $path) {
title
date (format: "MMMM D, Y")
content
tags {
title
path
}
}
}
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.post.title
    }
  }
}
</script>

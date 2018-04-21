<template>
  <div class="about-content">
    <h2>{{ title }}</h2>
    <p>{{ content }}</p>
  </div>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories/about', {
        version: 'draft'
    })
    .then(res => {
      // console.log(res.data.story.content)
      return {
        title: res.data.story.content.title,
        content: res.data.story.content.content
      }
    })
  }
}
</script>

<style scoped>
  .about-content {
    padding: 20px;
    width: 80%;
    max-width: 500px;
    margin: auto;
  }
  .about-content p {
  white-space: pre-line;
}
</style>

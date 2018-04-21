<template>
  <div id="post">
    <div class="post-thumbnail" :style="{backgroundImage: 'url(' + image + ')'}"></div>
    <section class="post-content">
      <h1>{{ title }}</h1>
      <p>{{ content }}</p>
    </section>
  </div>
</template>

<script>
export default {
    asyncData(context) {
        // debugger
        return context.app.$storyapi
            // console.log(context)
            .get('cdn/stories', {
                version: 'draft',
                starts_with: "blog/" + context.params.postid,
            }).then(res => {
                // console.log(res.data.stories[0].content)
                return {
                image: res.data.stories[0].content.Thumbnail,
                title: res.data.stories[0].content.Title,
                content: res.data.stories[0].content.Content
                };
            }).catch(error => {
                console.log(error)
            })
    }
};
</script>

<style>
.post-thumbnail {
  width: 100%;
  height: 300px;
  background-size: cover;
  background-position: center;
}
.post-content {
  width: 80%;
  max-width: 500px;
  margin: auto;
}
.post-content p {
  white-space: pre-line;
}
</style>
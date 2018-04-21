<template>
  <section id="posts">
    <PostPreview
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      :excerpt="post.previewText"
      :thumbnailImage="post.thumbnailUrl"
      :id="post.id" />
      <!-- <p>Title: {{title}}</p><br/>
      <h1>id: {{id}}</h1><br/>
      <p>thumbnailUrl: {{thumbnailUrl}}</p><br/>
      <h1>previewText: {{previewText}}</h1>
      <h1>Content: {{content}}</h1> -->
  </section>
</template>

<script>
import PostPreview from "@/components/Blog/PostPreview";
export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories",{
        version: "draft",
        starts_with: "blog/"
      })
      .then(res => {
        // console.log(res.data.stories[0])
        // return {
        //   title: res.data.stories[0].content.Title,
        //   id: res.data.stories[0].id,
        //   thumbnailUrl: res.data.stories[0].content.Thumbnail,
        //   previewText: res.data.stories[0].content.Summary,
        //   content: res.data.stories[0].content.Content,
        // }
        // console.log(res.data.stories)
        return {
          posts: res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.Title,
              previewText: bp.content.Summary,
              thumbnailUrl: bp.content.Thumbnail
            }
          })
        }
      })
  }

}

</script>

<style scoped>
#posts {
  padding-top: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
@media (min-width: 35rem) {
  #posts {
    flex-direction: row;
  }
}
</style>
<template>
  <div>
    <Loading v-if="$fetchState.pending"/>
    <p v-else-if="$fetchState.error"> ERROR</p>
    <div v-else>
      <img :src="`http://localhost:1337${blogs[0].image.url}`" alt="preview image" />
      <BlogHead :img="`http://localhost:1337${blogs[0].user_id.image.url}`"></BlogHead>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  apollo: {
    blogs: {
      query() {
        return gql`
          query clients($id:ID!) {
            client: blogs (where: { id: $id }) {
              id
              Name
              created_at
              image {
                url
              }
              user_id {
                id
                Name
                image{
                  url
                }
              }
            }
          }
        `;
      },
      variables() {
        return {
          id: this.$route.params.id,
        };
      },
      update: (blogs) => blogs.client,
    },
  },
};
</script>
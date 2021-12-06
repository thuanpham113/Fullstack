<template>
  <div>
    <Loading v-if="this.loading === 'true'"></Loading>

    <p v-else-if="this.loading === 'error'">Error</p>
    <div v-else>
      <img
        :src="`http://localhost:1337${blogs.image.url}`"
        alt="preview image"
      />
      <BlogHead
        :img="`http://localhost:1337${blogs.user_id.image.url}`"
        :title="blogs.Name"
        :name="blogs.user_id.Name"
        :date="blogs.created_at"
        :comment="blogs.comments"
      >
      </BlogHead>
      {{this.blogs.text}}
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  head() {
    return {
      title: "asyncData",
    };
  },
  data() {
    return {
      loading: true,
    };
  },
  apollo: {
    blogs: {
      query() {
        return gql`
          query clients($id: ID!) {
            client: blogs(where: { id: $id }) {
              id
              Name
              created_at
              text
              image {
                url
              }
              user_id {
                id
                Name
                image {
                  url
                }
              }
              comments {
                id
              }
            }
          }
        `;
      },
      variables() {
        // Use vue reactive properties here
        return {
          id: this.$route.params.id,
        };
      },
      update(data) {
        console.log(data);
        this.loading = false;
        // The returned value will update
        // the vue property 'pingMessage'
        return data.client[0];
      },
      error(error) {
        console.error("We've got an error!", error);
      },
      watchLoading(isLoading, countModifier) {
        console.log("loading");
        // isLoading is a boolean
        // countModifier is either 1 or -1
      },
    },
  },
};
</script>
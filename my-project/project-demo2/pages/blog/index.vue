<template>
  <v-card max-width="1000px" width="100vw" class="my-10 rounded-xl">
    <v-row align="center" justify="center">
      <v-col class="fill-height" align="center" justify="center">
        <v-card-title primary-title class="justify-center text-h1 pa-10">
          Blog
        </v-card-title>
        <v-breadcrumbs
          :items="breadcrumbs"
          divider="/"
          class="justify-center"
        ></v-breadcrumbs>
        <v-card
          v-for="(blog, index) in blogs"
          :key="blog.id"
          :number="index"
          width="80%"
          class="pa-5 my-5"
          color="transparent"
          outlined
        >
          <v-img
            :src="`http://localhost:1337${blog.image.url}`"
            class="ma-10"
          />
          <v-card-text>
            <div class="text-h3">
              {{ blog.Name }}
            </div>
            <div class="text-h6">
              {{
                new Date(blog.created_at).toLocaleDateString(undefined, {
                  weekday: "long",
                  year: "numeric",
                  month: "long",
                  day: "numeric",
                })
              }}
            </div>
            <div class="text-h6">
              {{ new Date(blog.created_at).toUTCString() }}
            </div>
          </v-card-text>
          <keep-alive>
            <NuxtLink :to="{ name: 'blog-id', params: { id: blog.id } }">
              <v-btn color="success" class="mb-5"> Read more </v-btn>
            </NuxtLink>
          </keep-alive>
        </v-card>
      </v-col>
    </v-row>
  </v-card>
</template>
<script>
import gql from "graphql-tag";
export default {
  head() {
    return {
      title: "Blog",
    };
  },
  name: "Blog",
  data() {
    return {
      breadcrumbs: [
        {
          text: "Home",
          disabled: false,
          href: "/",
        },
        {
          text: "Blog",
          disabled: false,
          href: "/Blog",
        },
      ],
    };
  },
  apollo: {
    blogs: {
      query() {
        return gql`
          query clients {
            client: blogs {
              id
              Name
              created_at
              image {
                url
              }
              user_id {
                id
                Name
              }
            }
          }
        `;
      },
      update: (blogs) => blogs.client,
    },
  },
};
</script>
<style lang="scss" scoped>
.body {
  height: auto;
  width: 100vw;
  align-items: center;
  justify-content: center;
  display: flex;
}
.contact {
  height: 100%;
  max-width: 1000px;
  background-color: bisque;
  margin: 100px;
}
header {
  align-items: center;
  justify-content: center;
  padding: 50px;
}
</style>
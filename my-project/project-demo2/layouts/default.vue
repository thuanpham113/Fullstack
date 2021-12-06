<template>
  <v-app app>
    <v-app-bar app flat color="transparent">
      <v-container color="transparent" class="py-0 fill-height">
        <button class="logo">
          <a href="/">
            <img :src="`http://localhost:1337${Homepages.Logo.url}`" alt="" />
          </a>
        </button>
        <v-btn
          v-for="title in Homepages.Text"
          :key="title.title"
          text
          class="list-menu"
          :href="`http://localhost:3000/${title.namelink}`"
        >
          {{ title.title }}
        </v-btn>

        <v-spacer></v-spacer>

        <v-responsive max-width="250px">
          <v-text-field
            class="hidden pa-5"
            dense
            flat
            hide-details
            append-icon="mdi-magnify"
            label="Search News"
            rounded
            solo-inverted
            v-model="Search"
            v-on:keyup.enter="toggleSearch(Search)"
          ></v-text-field>
        </v-responsive>
        <v-menu offset-y>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="" v-bind="attrs" v-on="on" class="list-menu__b">
              <v-icon>mdi-format-list-bulleted</v-icon>
            </v-btn>
          </template>
          <v-list height="90vh">
            <v-list-item>
              <v-list-item-title>
                <v-btn color="transparent" :href="`http://localhost:3000/`"
                  >Home</v-btn
                ></v-list-item-title
              >
            </v-list-item>
            <v-list-item v-for="(item, index) in Homepages.Text" :key="index">
              <v-list-item-title>
                <v-btn
                  color="transparent"
                  :href="`http://localhost:3000/${item.namelink}`"
                  >{{ item.title }}</v-btn
                ></v-list-item-title
              >
            </v-list-item>
          </v-list>
        </v-menu>
      </v-container>
    </v-app-bar>
    <v-main app>
      <div class="center">
        <Nuxt keep-alive />
      </div>
    </v-main>
    <v-footer dark padless>
      <v-card class="flex" flat tile>
        <v-card-title class="teal">
          <strong class="subheading"
            >Get connected with us on social networks!</strong
          >
          <v-spacer></v-spacer>
          <v-btn v-for="icon in icons" :key="icon" class="mx-4" dark icon>
            <v-icon size="24px">
              {{ icon }}
            </v-icon>
          </v-btn>
        </v-card-title>
        <v-card-text class="py-2 white--text text-center">
          {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
import gql from "graphql-tag";
export default {
  data: () => ({
    links: [
      { title: "Dashboard", link: "" },
      {
        title: "Messages",
        link: "",
      },
      { title: "Profile", link: "" },
      {
        title: "Updates",
        link: "",
      },
    ],
    icons: ["mdi-facebook", "mdi-twitter", "mdi-linkedin", "mdi-instagram"],
    Search: "",
    Homepages: [],
    toggleSearchs: false,
  }),
  apollo: {
    blog: {
      query() {
        return gql`
          query clients {
            client: userIds(where: { Jobs: { Title: "Design" } }) {
              id
              Name
              Jobs {
                id
              }
            }
          }
        `;
      },
      update: (datas) => datas.client,
    },
  },
  methods: {
    toggleSearch(value) {
      if (value != "") {
        this.toggleSearchs = true;
      }
    },
  },
  apollo: {
    Homepages: {
      query: gql`
        query clients {
          client: homepage {
            name
            Logo {
              url
            }
            Text {
              namelink
              title
            }
          }
        }
      `,
      update: (Homepages) => Homepages.client,
    },
  },
};
</script>
<style scoped>
#app {
  background-color: azure;
}
.logo {
  position: relative;
  width: 100px;
  overflow: hidden;
  display: flex;
  align-items: center;
}
.center {
  display: flex;
  justify-content: center;
  align-self: center;
}
img {
  height: 50px;
}
.v-btn.list-menu__b {
  overflow: hidden;
  padding: 0;
  min-width: 0px;
  height: 0;
}
@media (max-width: 800px) {
  .v-btn.list-menu {
    min-width: 0;
    width: 0;
    padding: 0;
    overflow: hidden;
  }
  .v-btn.list-menu__b {
    width: 40px;
    overflow: auto;
    height: 40px;
  }
}

.v-main {
  background-color: #333;
  align-items: center;
  justify-content: center;
  padding: 0;
}
</style>
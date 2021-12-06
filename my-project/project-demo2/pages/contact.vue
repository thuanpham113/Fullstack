<template>
  <div style="justify-content: center; display: flex">
    <v-card max-width="800px" class="pa-5 ma-5">
      <v-col>
        <v-card-title primary-title class="text-h3">
          Contact our sales team
        </v-card-title>
        <v-card-text class="text-h6">
          Our sales team is at your disposal to discuss your project. Fill out
          the form below and we will get back to you as soon as possible.
        </v-card-text>

        <v-form @submit.prevent="submit" class="pa-10">
          <v-row justify-space-around>
            <v-text-field
              v-model="form.first"
              label="First name"
              required
            ></v-text-field>
            <v-text-field
              v-model="form.last"
              label="Last name"
              required
            ></v-text-field>
          </v-row>
          <v-row>
            <v-text-field
              v-model="form.bussiness"
              label="Bussiness Email"
              tile
            ></v-text-field>
            <v-text-field
              v-model="form.company"
              label="Company Name"
              tile
            ></v-text-field>
          </v-row>
          <v-col class="d-flex mt-5">
            <v-select
              :items="items"
              label="How can we help you get started"
              v-model="form.select"
              class="ma-0"
              menu-props="offset-y"
            ></v-select>
          </v-col>
          <input type="checkbox" id="label1" v-model="checkbox" />
          <label for="label1">
            By completing this form, I have read and acknowledged the
            <a href="https://www.threekit.com/privacy-policy">Privacy Policy</a>
            and agree that Synode may contact me at the email address or phone
            number above.
          </label>
        </v-form>
        <v-btn
          color="indigo accent-4"
          class="ma-10 ml-16"
          :disabled="!formIsValid"
          @click="submit"
          >submit</v-btn
        >
      </v-col>
    </v-card>
  </div>
</template>
<script>
import SynodeHoverInput from "../components/SynodeHoverInput.vue";
export default {
  components: { SynodeHoverInput },
  computed: {
    formIsValid() {
      if (this.checkbox) {
        return true;
      } else {
        return false;
      }
    },
  },

  data() {
    const defaultForm = Object.freeze({
      first: "",
      last: "",
      bussiness: "",
      company: "",
      select: "",
    });

    return {
      form: {
        first: "",
        last: "",
        bussiness: "",
        company: "",
        select: "",
      },
      defaultForm,
      checkbox: null,
      items: [
        "I'd lite to schedule a demo",
        "I'm looking for pricing",
        "I'have a question",
        "Order",
      ],
    };
  },
  methods: {
    resetForm() {
      this.form = Object.assign({}, this.defaultForm);
      this.checkbox = null;
    },
    submit() {
      this.resetForm();
    },
  },
};
</script>

<style lang="scss" scoped>
.v-text-field {
  margin: 10px;
}
</style>
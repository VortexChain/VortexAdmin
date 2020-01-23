<template>
  <div>
    <div class="display-1	mb-5">Welcome to VortexAdmin</div>
    <v-row>
      <v-col
        v-for="(page, index) in pages"
        :key="index"
        cols="12"
        sm="6"
        md="4"
        lg="3"
      >
        <v-card v-ripple class="item-card">
          <nuxt-link
            :to="page.route"
            tag="div"
            class="pa-5 d-flex flex-column align-start"
          >
            <div class="subtitle-1">{{ page.name }}</div>
            <div class="caption">Lorem, ipsum dolor</div>
            <v-icon class="mt-auto">{{ page.icon }}</v-icon>
          </nuxt-link>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card v-ripple class="item-card">
          <div
            @click="dialog = true"
            class="pa-5 d-flex flex-column align-center justify-center"
          >
            <v-icon>mdi-plus </v-icon>
            <div class="subtitle-1">Add tab</div>
          </div>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog v-model="dialog" persistent max-width="290">
      <v-card>
        <v-card-title class="headline"
          >Use Google's location service?</v-card-title
        >
        <v-card-text
          >Let Google help apps determine location. This means sending anonymous
          location data to Google, even when no apps are running.</v-card-text
        >
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn @click="dialog = false" color="green darken-1" text
            >Disagree</v-btn
          >
          <v-btn @click="dialog = false" color="green darken-1" text
            >Agree</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      dialog: false,
      pages: [
        {
          name: 'Active servers',
          icon: 'mdi-server-security',
          route: '/servers'
        }
      ]
    }
  }
}
</script>

<style lang="less" scoped>
.item-card {
  height: 220px;
  cursor: pointer;

  > div {
    height: 100%;
  }
}
</style>

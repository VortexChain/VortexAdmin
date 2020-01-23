<template>
  <v-card>
    <!-- <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title> -->
    <v-data-table
      :headers="headers"
      :items="sshServers"
      :items-per-page="5"
      :loading="loading"
      :search="search"
      class="elevation-1"
      loading-text="Loading... Please wait"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-text-field
            v-model="search"
            prepend-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
            class="mr-5"
          ></v-text-field>
          <v-dialog max-width="500px">
            <template v-slot:activator="{ on }">
              <v-btn v-on="on" color="primary">New server</v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="headline">New server</span>
              </v-card-title>
            </v-card>
          </v-dialog>
          <v-btn @click="loadServers" class="ml-2" text icon>
            <v-icon>mdi-refresh</v-icon>
          </v-btn>
          <v-menu bottom left>
            <template v-slot:activator="{ on }">
              <v-btn v-on="on" icon>
                <v-icon>mdi-dots-vertical</v-icon>
              </v-btn>
            </template>

            <v-list>
              <v-list-item
                v-for="(item, i) in ['Параметры хеширования', 'Item 2']"
                :key="i"
                @click="loadServers"
              >
                <v-list-item-title>{{ item }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </v-toolbar>
      </template>
      <template v-slot:item.system="{ item }">
        <v-icon v-if="item.system.toLowerCase().includes('windows')"
          >mdi-windows</v-icon
        >
        <v-icon v-else-if="item.system.toLowerCase().includes('ubuntu')"
          >mdi-ubuntu</v-icon
        >
        <v-icon v-else-if="item.system.toLowerCase().includes('mac')"
          >mdi-apple</v-icon
        >
        <span style="vertical-align: middle;">{{ item.system }}</span>
      </template>
      <template v-slot:header.expand></template>
      <template v-slot:item.expand="{ item }">
        <div style="text-align: right;">
          <v-icon @click="editServer" small class="mr-2">
            mdi-pencil
          </v-icon>
          <v-icon @click="openDeleteModal(item)" small>
            mdi-delete
          </v-icon>
        </div>
      </template>
    </v-data-table>
    <v-dialog v-model="deleteDialog" max-width="290">
      <v-card v-if="deletedItem" :loading="deletingItem">
        <v-card-title class="headline">Delete this server</v-card-title>
        <v-card-text
          >Lorem ipsum, dolor sit amet consectetur adipisicing elit. Illo
          laboriosam atque dolorum tempora veritatis dignissimos fuga,
          aliquid.</v-card-text
        >
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn @click="deleteDialog = false" text>Cancel</v-btn>
          <v-btn @click="deleteServer(deletedItem.id)" color="red darken-1" text
            >Delete</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      loading: true,
      sshServers: [],
      search: '',
      deleteDialog: false,
      deletedItem: null,
      deletingItem: false,
      headers: [
        { text: 'Name', value: 'name' },
        { text: 'System', value: 'system' },
        { text: 'Host', value: 'host' },
        { text: 'Actions', value: 'expand', sortable: false }
      ]
    }
  },
  created() {
    this.loadServers()
  },
  methods: {
    loadServers() {
      this.loading = true
      this.$axios.$get('api/GetSshServers').then((servers) => {
        this.sshServers = servers
        this.loading = false
      })
    },
    editServer(id, params) {},
    openDeleteModal(item) {
      this.deletedItem = item
      this.deleteDialog = true
    },
    deleteServer(id) {
      console.log(id)
      this.deletingItem = true
      setTimeout(() => {
        this.deletingItem = false
        this.deleteDialog = false
      }, 1000)
    }
  }
}
</script>

<style></style>

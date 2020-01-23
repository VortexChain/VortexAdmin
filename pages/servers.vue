<template>
  <div class="mx-3">
    <div class="display-1	mb-5">Servers</div>
    <v-tabs v-model="tab" background-color="transparent">
      <v-tab>All instances</v-tab>
      <v-tab>World map</v-tab>
      <v-tab>Add once</v-tab>
    </v-tabs>
    <v-tabs-items v-model="tab" class="mt-5">
      <v-tab-item>
        <servers-table />
      </v-tab-item>
      <v-tab-item>
        <v-card>
          <v-card-text>World map</v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card>
          <v-card-text>Add once</v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </div>
</template>

<script>
export default {
  name: 'Servers',
  components: {
    ServersTable: () => import('@/components/servers/servers-table')
  },
  data() {
    return {
      tab: null
    }
  }
}
</script>

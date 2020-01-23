<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      src="https://www.gstatic.com/mobilesdk/190424_mobilesdk/nav_nachos@2x.png"
      color="#051e34"
      overlay-color="white"
      fixed
      app
    >
      <div class="nav-draw-title">
        <i class="vortex-icon"></i>
        <span class="vortex-title"
          >Vortex<span style="color: #ffcb2b;">Admin</span></span
        >
      </div>
      <v-expansion-panels accordion tile multiple dark flat>
        <v-expansion-panel
          v-for="(el, i) in items"
          :key="i"
          :class="miniVariant ? 'mini' : ''"
          class="list-item"
        >
          <v-expansion-panel-header v-if="!miniVariant">{{
            el.group
          }}</v-expansion-panel-header>
          <v-expansion-panel-content class="list-item-content">
            <v-list class="pa-0" dark>
              <v-list-item
                v-for="(item, index) in el.items"
                :key="index"
                :to="item.to"
                router
                exact
              >
                <v-list-item-action>
                  <v-icon>{{ item.icon }}</v-icon>
                </v-list-item-action>
                <v-list-item-content>
                  <v-list-item-title v-text="item.title" />
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      elevate-on-scroll
      fixed
      app
      color="#eceff1"
      height="48px"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer />
    </v-app-bar>
    <v-content class="content">
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <!-- <v-footer :fixed="fixed" app>
      <span>&copy; 2019</span>
    </v-footer> -->
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [
        {
          group: 'Vortex',
          items: [
            {
              icon: 'mdi-thermostat',
              title: 'Status',
              to: '/'
            },
            {
              icon: 'mdi-database',
              title: 'Databases',
              to: '/inspire'
            }
          ]
        },
        {
          group: 'Develop',
          items: [
            {
              icon: 'mdi-apps',
              title: 'Welcome',
              to: '/'
            },
            {
              icon: 'mdi-chart-bubble',
              title: 'Inspire',
              to: '/inspire'
            }
          ]
        },
        {
          group: 'Service',
          items: [
            {
              icon: 'mdi-apps',
              title: 'Dedicated servers',
              to: '/servers'
            }
          ]
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'VortexAdmin'
    }
  }
}
</script>

<style lang="less" scoped>
.nav-draw-title {
  width: 100%;
  height: 48px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  cursor: pointer;
  color: white;

  &:hover .vortex-icon {
    transform: rotate(360deg);
  }

  .vortex-icon {
    margin-left: 20px;
    height: 28px;
    width: 28px;
    transition: 1s;
    color: #ffcb2b;
  }

  .vortex-title {
    margin-left: 12px;
    font-size: 20px;
    font-family: 'Product Sans Regular', sans-serif;
  }
}

.list-item {
  background: transparent !important;
  color: white !important;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);

  &.mini {
    border-bottom: 0px solid rgba(255, 255, 255, 0.2);
  }
}

.content {
  background-color: #eceff1;
}
</style>

<style>
.list-item-content > div {
  padding-left: 0;
  padding-right: 0;
}
</style>

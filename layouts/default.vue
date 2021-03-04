<template>
  <v-app dark>
    <v-navigation-drawer
    class="primary"
    dark
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          :target="item.external"
          router
          exact
        >
          <v-list-item-action >
            <v-icon >{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      
      class="white"
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <!-- <v-btn
        icon
        @click.stop="clipped = !clipped"
      >
        <v-icon>mdi-application</v-icon>
      </v-btn> -->
      <!-- <v-btn
        icon
        @click.stop="fixed = !fixed"
      >
        <v-icon>mdi-minus</v-icon>
      </v-btn> -->
      <!-- <v-toolbar-title v-text="title" /> -->
        <img src="https://wewatch.ae/wp-content/uploads/2020/03/logo-web.png" />
      <v-spacer />
      <v-btn @click="logout" icon color="secondary">
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed
    >
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer 
      dark
      class="grey"
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: true,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Dashboard',
          to: '/'
        },
        // {
        //   icon: 'mdi-chart-bubble',
        //   title: 'Report',
        //   to: '/report'
        // },

        {
          icon: 'mdi-chart-bubble',
          title: 'Super Admin',
          to: '/super_admin',
         },
       
         {
          icon: 'mdi-chart-bubble',
          title: 'wewatch Manager',
          to: '/wewatchmanager'
        },
         {
          icon: 'mdi-chart-bubble',
          title: 'User',
          to: '/User'
        },
         {
          icon: 'mdi-chart-bubble',
          title: 'Security User',
          to: '/security_guard'
        },

        {
          icon: 'mdi-chart-bubble',
          title: 'Client',
          to: '/client'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Project',
          to: '/project'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Allocation',
          to: '/allocations'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'HSE',
          to: '/reports/hse',
          external : '_blank',
        }
        ,
        {
          icon: 'mdi-chart-bubble',
          title: 'Securtiy',
          to: '/reports/security',
          external : '_blank',
        }       
        
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'wewatch.ae'
    }
  },
  methods:{
     logout() {
       this.$auth.logout();
},
  }
}
</script>

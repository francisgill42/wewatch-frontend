<template>
  <v-row>
      <!-- <v-col cols="12" sm="8" md="4" >
      <v-card class="pa-5">
      <Chart />
      </v-card>
       </v-col>
       <v-col cols="12" sm="8" md="4" >
      <v-card class="pa-5">
        <PieChart />
      </v-card>
       </v-col>
       <v-col cols="12" sm="8" md="4" >
      <v-card class="pa-5">
      </v-card>
       </v-col> -->
   <v-col cols="12" sm="8" md="12">
    
 
       <v-card>
        <v-card-title class="headline">
          Welcome to the wewatch dashboard
        </v-card-title>
        <v-card-text>
         
        
      
        
          <p>We are looking forward to bringing more exciting features in the future.</p>
          <!-- <div class="text-xs-right">
            <em><small>&mdash; John Leider</small></em>
          </div> -->
          <!-- <hr class="my-3">
          <a
            href="https://nuxtjs.org/"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt Documentation
          </a>
          <br>
          <a
            href="https://github.com/nuxt/nuxt.js"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt GitHub
          </a> -->
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
// import Chart from '~/components/Chart.vue'
// import PieChart from '~/components/PieChart.vue'

export default {
  components: {
    // Chart,
    // PieChart
  }
}
</script>

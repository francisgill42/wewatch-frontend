<template>
<div>
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
          <v-col  cols="12" sm="8" md="4" v-for="(card,i) in cards" :key="i">
            <v-card :class="card.color" class="pa-2">
            <v-list-item dark>
            <v-list-item-content>
            <div class="text-center">{{added_zero(card.count)}}</div>
            <div class="text-center" v-text="card.text"></div>
            </v-list-item-content>
            </v-list-item>
            </v-card>
          </v-col>
           
  </v-row>
  <!-- <v-row>
     <v-col  cols="12" sm="8" md="4" v-for="(card,i) in second_cards" :key="i">
            <v-card :class="card.color" class="pa-3">
            <v-list-item dark>
            <v-list-item-content>
            <div class="text-center">{{added_zero(card.count)}}</div>
            <div class="text-center" v-text="card.text"></div>
            </v-list-item-content>
            </v-list-item>
            </v-card>
          </v-col>
  </v-row> -->
  <v-row>
  
  <v-col cols="6">
      <client-only>
        <DoughnutChart :data="data" :height="200" />
      </client-only>
  </v-col>
    <v-col cols="6">
        <client-only>
        <LineChart :data="data" :height="200" />
      </client-only>

  </v-col>
    <v-col cols="6">
        <client-only>
          <PieChart :data="data" :height="200" />
      </client-only>
        </v-col>
  <v-col cols="6">
        <client-only>
          <BarChart :data="data" :height="200" />      
        </client-only>

  </v-col>
</v-row>

</div>
</template>

<script>
// import Chart from '~/components/Chart.vue'
// import PieChart from '~/components/PieChart.vue'

export default {

  components: {
    // Chart,
    // PieChart
  },
  methods : {
    added_zero(v) { return v < 10 ? '0' + v : v }
  },
 data : () => ({
   cards : [
    {text:'Accident Incident Report',count:9,icon:'mdi-home',color:'primary'},
    {text:'Covid-19 Register',count:15,icon:'mdi-home',color:'blue'},
    {text:'Daily Security Report',count:23,icon:'mdi-home',color:'info lighten-1'},
    {text:'Daily HSE Report',count:559,icon:'mdi-home',color:'orange darken-4 '},
    {text:'Daily Site Visiter Register',count:199,icon:'mdi-home',color:'brown darken-1'},
    {text:'Daily Site Visiter Register',count:199,icon:'mdi-home',color:'brown darken-1'},
    {text:'Daily Site Visiter Register',count:199,icon:'mdi-home',color:'brown darken-1'},
    {text:'Lost Work Hours',count:523,icon:'mdi-home',color:'brown lighten-1'},
    {text:'Daily Man Hours',count:125,icon:'mdi-home',color:'orange lighten-1 '},

   ],
   second_cards : [
      // {text:'Daily Man Hours',count:125,icon:'mdi-home',color:'orange lighten-1 '},
      // {text:'Daily Site Visiter Register',count:199,icon:'mdi-home',color:'brown darken-1'},
      // {text:'Lost Work Hours',count:523,icon:'mdi-home',color:'brown lighten-1'},
   ],
    data: {
        labels: [],
          
        datasets: [
          {
            label: 'checking',
            backgroundColor: [],
            data: [],
           
          }
        ]
      },
 }),
   mounted(){
    var arr = [
       {text:'Accident Incident Report',count:9},
        {text:'Covid-19 Register',count:15},
        {text:'Daily Security Report',count:23},
        {text:'Daily HSE Report',count:559},
        {text:'Daily Man Hours',count:125},
        {text:'Daily Site Visiter Register',count:199},
        {text:'Lost Work Hours',count:523},
    ];


    this.data.labels = arr.flatMap((v) => v.text)
    this.data.datasets[0].data = arr.flatMap((v) => v.count)
    
    // this.data.datasets[0].label = 'francis'
    this.data.datasets[0].backgroundColor = [
            'rgb(54, 162, 235)',
            'rgb(255, 99, 132)',
            'rgb(75, 192, 192)',
            'rgb(255, 159, 64)',
            'rgb(201, 203, 207)',
            'rgb(153, 102, 255)',
            'rgb(255, 205, 86)'
    ]
    
  },


 
}
</script>

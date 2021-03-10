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
          <v-col  cols="12" sm="8" md="4" class="" v-for="(card,i) in cards" :key="i">
            <v-card :to="card.link" :class="card.color" class="pa-2">
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
        <DoughnutChart v-if="loaded" :data="data" :options="options" :height="200" />
  </v-col>
  <v-col cols="6">
        <LineChart v-if="loaded" :data="data" :options="options"  :height="200" />
  </v-col>
  <v-col cols="6">
        <PieChart v-if="loaded" :data="data" :options="options"  :height="200" />
  </v-col>  
  <v-col cols="6">
        <BarChart v-if="loaded" :data="data" :options="options"  :height="200" />
  </v-col>
</v-row>

</div>
</template>

<script>
export default {

  methods : {
    added_zero(v) { return v < 10 ? '0' + v : v }
  },
 data : () => ({
    loaded : false,
    arr : [],
    cards : [],
    value: [],
    data: {
        labels: [],
          
        datasets: [
          {
            backgroundColor: [],
            data: [],
          },          
        ],
      },
      options : {
            showLines: false,
          }
 }),
   async mounted () {
    this.loaded = false
    try {
      await this.$axios.get('all')
      .then(res => {
        
        this.cards = [
                    {link : '/accidentincident',text:'Accident Incident Report',count:res.data.GetAccidentIncidentCount,color:'primary',chartColor : 'rgb(45 87 163)'},
                    {link : '/covid',text:'Covid-19 Report',count:res.data.GetCovidCount,color:'red',chartColor : 'rgb(244 67 54)'},
                    {link : '/security',text:'Daily Security Report',count:res.data.GetDailySecurityReportCount,color:'info lighten-1',chartColor : 'rgb(75 194 181)'},
                    {link : '/hse',text:'Daily HSE Report',count:res.data.GetDailyHSEReportCount,color:'orange darken-4', chartColor : 'rgb(230 81 0)'},
                    {link : '/sitevisitor',text:'Daily Site Visiter Report',count:res.data.GetSiteVisiterRecordCount,color:'brown darken-1',chartColor : 'rgb(109 76 65)'},
                    {link : '/traininginduction',text:'Training Induction Report',count:res.data.GetTrainingInductionCount,color:'purple',chartColor : 'rgb(156 39 176)'},
                    {link : '/observation',text:'Observation Report',count:res.data.GetObservationCount,color:'green',chartColor : 'rgb(76 175 80)'},
                    // {link : '/covid',text:'Daily Man Hours',count:res.data.GetDailyManHoursCount,color:'orange lighten-1',chartColor : 'rgb(255 167 38)'},
                    // {link : '/covid',text:'Lost Work Hours',count:res.data.GetLostWorkHoursCount,color:'brown lighten-1',chartColor : 'rgb(141 110 99)'},

        ];
        this.data.labels = this.cards.flatMap((v) => v.text )
        this.data.datasets[0].label = 'Reports'
        this.data.datasets[0].data = this.cards.flatMap((v) => v.count )
        this.data.datasets[0].backgroundColor = this.cards.flatMap((v) => v.chartColor )
      });

      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>

<template>
<v-row>
      <v-col  cols="12" sm="8" md="6" class="" v-for="(card,i) in cards" :key="i">
                         
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
</template>

<script>
  export default {
    data: () => ({ cards : [] }),

 
    created () {
       this.$axios.get('all').then(res => {
        
        this.cards = [
                    {text:'Accident Incident Report',count:res.data.GetAccidentIncidentCount,color:'primary',link : '/accidentincident'},
                    {text:'Covid-19 Report',count:res.data.GetCovidCount,color:'red',link : '/covid'},
                    {text:'Daily Security Report',count:res.data.GetDailySecurityReportCount,color:'info lighten-1',link : '/reports/security'},
                    {text:'Daily HSE Report',count:res.data.GetDailyHSEReportCount,color:'orange darken-4',link : '/hse'},
                    {text:'Daily Site Visiter Report',count:res.data.GetSiteVisiterRecordCount,color:'brown darken-1',link : '/reports/sitevisitor'},
                    {text:'Training Induction Report',count:res.data.GetTrainingInductionCount,color:'purple',link : '/traininginduction'},
                    {text:'Observation Report',count:res.data.GetObservationCount,color:'green',link : '/observation'},
                    // {text:'Daily Man Hours',count:res.data.GetDailyManHoursCount,color:'orange lighten-1',link : '/reports/hse'},
                    // {text:'Lost Work Hours',count:res.data.GetLostWorkHoursCount,color:'brown lighten-1',link : '/reports/hse'},

        ];


      });
    },

    methods: {
     
      added_zero(v) { return v < 10 ? '0' + v : v },
  
    },
  }
</script>
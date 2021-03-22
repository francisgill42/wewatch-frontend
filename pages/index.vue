<template>
<div>
    <v-row>

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

          <v-col md="12">
            <Allocations />
          </v-col>
           
  </v-row>

</div>
</template>

<script>
import Allocations from '@/components/Allocations';
export default {

  components : { Allocations },

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
                    {link : '/project',text:'Total Projects',count:res.data.ProjectCount,color:'primary',chartColor : 'rgb(45 87 163)'},
                    {link : '/project_admin',text:'Total Project Admins (Clients)',count:res.data.ProjectAdminCount,color:'green',chartColor : 'rgb(45 87 163)'},
                    {link : '/wewatchmanager',text:'Total Wewatch Managers',count:res.data.WewatchManagerCount,color:'purple',chartColor : 'rgb(244 67 54)'},
                    {link : '/user',text:'Total Users',count:res.data.UserCount,color:'info lighten-1',chartColor : 'rgb(75 194 181)'},
                    {link : '/security_guard',text:'Total Security Guard',count:res.data.SecurityGuardCount,color:'orange darken-4', chartColor : 'rgb(230 81 0)'},
                    // {link : '/covid',text:'Daily Man Hours',count:res.data.GetDailyManHoursCount,color:'orange lighten-1',chartColor : 'rgb(255 167 38)'},
                    // {link : '/covid',text:'Lost Work Hours',count:res.data.GetLostWorkHoursCount,color:'brown lighten-1',chartColor : 'rgb(141 110 99)'},

        ];
        // this.data.labels = this.cards.flatMap((v) => v.text )
        // this.data.datasets[0].label = 'Reports'
        // this.data.datasets[0].data = this.cards.flatMap((v) => v.count )
        // this.data.datasets[0].backgroundColor = this.cards.flatMap((v) => v.chartColor )
      });

      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>

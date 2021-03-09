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
    data: () => ({

      entity : 'Security Guards',  
      dialog: false,
      isActive: true,
      search:'',
       cards : [],
      headers: [
        {
          text: 'Name',
          sortable: true,
          value: 'name',
        },
        {
          text: 'Email',
          sortable: false,
          value: 'email',
        },
        // {
        //   text: 'Mobile No',
        //   sortable: false,
        //   value: 'mobile_no',
        // },
        {
          text: 'Active',
          sortable: true,
          value: 'isactive',
        },
        { text: 'Actions', value: 'actions', sortable: false },

      ],
      data: [],
      editedIndex: -1,
      editedItem: {
      role_id: 7,
      name: "",
      email: "",
      password: "",
      confirm_password: "",
      mobile_no: "",
      },
      defaultItem: {
      role_id: 7,
      department_id : "",
      name: "",
      email: "",
      password: "",
      confirm_password: "",
      mobile_no: "",
      confirm_password: ""
      },
      change_password: "",
      errors:[],
      Rules : [
          v => !!v || 'This field is required',
        ],

    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New' : 'Edit'
      },
    },

  
    created () {
      this.initialize()
    },

    methods: {
     
      added_zero(v) { return v < 10 ? '0' + v : v },

      initialize () {
        this.$axios.get('all')
      .then(res => {
        
        this.cards = [
                    {text:'Accident Incident Report',count:res.data.GetAccidentIncidentCount,color:'primary',link : '/reports/hse'},
                    {text:'Covid-19 Report',count:res.data.GetCovidCount,color:'red',link : '/hse'},
                    {text:'Daily Security Report',count:res.data.GetDailySecurityReportCount,color:'info lighten-1',link : '/reports/hse'},
                    {text:'Daily HSE Report',count:res.data.GetDailyHSEReportCount,color:'orange darken-4',link : '/reports/hse'},
                    {text:'Daily Site Visiter Report',count:res.data.GetSiteVisiterRecordCount,color:'brown darken-1',link : '/reports/hse'},
                    {text:'Training Induction Report',count:res.data.GetTrainingInductionCount,color:'purple',link : '/reports/hse'},
                    {text:'Observation Report',count:res.data.GetObservationCount,color:'green',link : '/reports/hse'},
                    // {text:'Daily Man Hours',count:res.data.GetDailyManHoursCount,color:'orange lighten-1',link : '/reports/hse'},
                    // {text:'Lost Work Hours',count:res.data.GetLostWorkHoursCount,color:'brown lighten-1',link : '/reports/hse'},

        ];


      });


      
      },



      
  
    },
  }
</script>
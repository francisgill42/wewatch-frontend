<template>
  <v-data-table
    :headers="headers"
    :items="data"
    :search="search"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat color="white">
        <v-toolbar-title>{{entity}}</v-toolbar-title>
      
        <v-text-field   
          class="mx-4"
        label="Search"
        hide-details v-model="search"></v-text-field>
         
      </v-toolbar>
    </template>
    <template v-slot:item.image="{ item }">


        <img height="150px" width="150px"  :src="item.image" />

    </template>

    <template v-slot:item.actions="{ item }">
      <!-- <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon> -->
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn small color="primary" @click="initialize">Reset</v-btn>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    data: () => ({

      entity : 'Daily Site Visitor',  
      dialog: false,
      isActive: true,
      search:'',
      headers: [
     
        //  {
        //   text: 'project',
        //   sortable: true,
        //   value: 'project_id',
        // },
        // {
        //   text: 'user',
        //   sortable: true,
        //   value: 'user_id',
        // },
         {
          text: 'company',
          sortable: true,
          value: 'company_name',
        },

         {
          text: 'driver',
          sortable: true,
          value: 'driver_contact',
        },
        
         {
          text: 'visit reason',
          sortable: true,
          value: 'visit_reason',
        },
        //   {
        //   text: 'car attachment',
        //   sortable: true,
        //   value: 'car_attachment',
        // },
        //  {
        //   text: 'id attachment',
        //   sortable: true,
        //   value: 'id_attachment',
        // },

       
        { text: 'Action', value: 'actions', sortable: false },

      ],
      data: [],
      editedIndex: -1,
      editedItem: {
      role_id: 5,
      name: "",
      email: "",
      password: "",
      confirm_password: "",
      mobile_no: "",
      },
      defaultItem: {
      role_id: 5,
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

    watch: {
      dialog (val) {
        val || this.close()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {

      this.$axios.get(`dailyvisitorsregister`).then(res => {
        console.log(res.data);
        console.log(this.data = res.data);
      });

      
      },

      editItem (item) {
        this.editedIndex = this.data.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.isActive = item.isactive
        this.errors = []
        this.dialog = true
      },

      deleteItem (item) {
       
         confirm('Are you sure you want to delete this item?') && 
         this.$axios.delete('accidentincident/'+item.id)
            .then((res) => {
     
              const index = this.data.indexOf(item)
              this.data.splice(index, 1)
            
            });
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

    

      
     
    },
  }
</script>
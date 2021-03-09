<template>

  <div>
    <v-toolbar flat>
    <v-text-field v-model="search" placeholder="search"></v-text-field>

    </v-toolbar>
    
  <v-data-table
    :headers="headers"
    :items="data"
    :search="search"
    class="elevation-1"
  >
   <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
</v-data-table>
  </div>


</template>

<script>
  export default {
    data: () => ({

      entity : 'HSE',  
  
      search:'',
      headers: [
        {
          text: '#',
          sortable: true,
          value: 'id',
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

      this.$axios.get(`covid`)
        .then(res => {
          this.data = res.data.data;
         });

      
      },
    },
  }
</script>
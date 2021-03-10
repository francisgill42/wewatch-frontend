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
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-text-field   
        label="Search"
        hide-details v-model="search"></v-text-field>
         <!-- <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider> -->
        <v-dialog v-model="dialog" max-width="900px">
          <template v-slot:activator="{ on }">
            <v-btn small dark class="secondary mb-2" v-on="on">Add {{entity}}</v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }} {{entity}}</span>
               <v-spacer></v-spacer>
               
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                   

                  <!-- <v-col cols="6" sm="6" md="12">
                    <v-text-field v-model="editedItem.name" :label="`${entity} Name`"></v-text-field>
                    <div style="color:red;" v-if="errors.name">{{errors.name[0]}}</div>
                  </v-col> -->
                 
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn small class="primary" text @click="close">Cancel</v-btn>
              <v-btn small class="secondary" text @click="save">Save</v-btn>
              
            </v-card-actions>

            <template v-if="editedIndex > -1">

            <v-divider></v-divider>

              
            <v-card-title>
              <span class="headline">Password Update</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                 <v-form
                      ref="change_password_ref"
                      lazy-validation
                      >
                     <v-text-field autocomplete="on" :rules="Rules" type="password" v-model="change_password" label="New Password"></v-text-field>
                     <v-btn small class="primary" text @click="close">Cancel</v-btn>
                     <v-btn small class="secondary" text @click="change_password_func">Save</v-btn>
                
              
                    </v-form>
              </v-container>
            </v-card-text>


            </template>

          </v-card>

        </v-dialog>
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

      entity : 'Observation',  
      dialog: false,
      isActive: true,
      search:'',
      headers: [
        {
          text: 'Project',
          sortable: true,
          value: 'project.project_name',
        },
         {
          text: 'Action',
          sortable: true,
          value: 'action',
        },
         
       
        { text: '', value: 'actions', sortable: false },

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

      this.$axios.get(`observation`).then(res => this.data = res.data);

      
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
         this.$axios.delete('observation/'+item.id)
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

    

      save () {

        var payload = {
                        "project_id": 1,
                        "user_id": 1,
                        "observation_description": null,
                        "action": "test2",
                        "attachments": "http://localhost:8000/uploads/obserations/ORD_CUP.jpg",

    };
       
          
              this.$axios.post('observation',payload)
              .then((res) => {
                   
                    if(res.data.success){
                      this.data.push(res.data.data)
                      this.close()
                      this.errors = []
                      }
                      else{
                        this.errors = res.data.errors
                        }
            })
            .catch(err => console.log(this.errors = err.response.data.errors));
        }
     
    },
  }
</script>
<template>
  <v-container>
    <data-table
      :options="options"
      :title="title"
      :headers="headers"
      :data="data"
      class="custom-table"
      @addRecord="addRecord"
      @deleteRecord="deleteRecord($event)"
      @reloadtable="initialize()"
      @FilterBy="filterBy($event)"
      @updatePagenum="updatePagenum($event)"
    >
      <template v-slot:status="{item}">
        <v-switch
          inset
          color="success"
          dense
          hide-details=""
        ></v-switch>
      </template>
    </data-table>
  </v-container>
</template>
<script>
import dataTable from "~/components/ui/dataTable.vue";
import tableHelper from "~/mixins/tableHelper.vue";
export default {
  components: { dataTable },
  mixins:[tableHelper],
  data() {
    return {
      options: {},
      title: "Users",
      headers: [
        {
          text: "#",
          value: "id",
          width:'2%',
        },
        {
          text: "First name",
          value: "first_name",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Middle name",
          value: "middle_name",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Last name",
          value: "last_name",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Birthday",
          value: "birth_date",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Address",
          value: "address",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Email",
          value: "email",
          filterable:true,
          sortType:null,
          filterValue:'',
        },
        {
          text: "Password",
          value: "password",
        },
        {
          text: "Account Type",
          value: "account_type",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "License Number",
          value: "license_number",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Mobile Number",
          value: "mobile_number",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Email Verified",
          value: "email_verified",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Number Verified",
          value: "number_verified",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Account Verified",
          value: "account_verified",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Active Status",
          value: "active_status",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Total Trip",
          value: "total_trip",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Rating",
          value: "rating",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Documents",
          value: "document",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Photo",
          value: "photo",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Action",
          value: "action"
        },
      ],
      data: [],
      drawer1:false
    };
  },
  mounted() {
    this.initialize()
  },
  methods: {
    initialize() {
      this.$axios.get(`getUnverifiedUsers`).then(({data}) => {
        this.data = data.data
        this.options = data.options
      })
    },
    getUsers(){s
      this.$axios.get(`getUnverifiedUsers`).then(({data}) => {
        this.data = data.data
      })
    },
    addRecord() {
      // this.goTo('clients-create')
      // this.$root.dialog(
      //   "Confirm Message!",
      //   "Are you sure you want to add this record ?",
      //   "c"
      // )
      //   .then(() => {});
    },
    deleteRecord(items) {
        let ids = this.getIds(items)
        this.$axios.delete(`getUnverifiedUsers/${ids}`).then(({data}) => {
          this.successNotification(items, 'deleted', 'users', 'users', 'users')
          this.initalize()
        })

    },
  },
};
</script>

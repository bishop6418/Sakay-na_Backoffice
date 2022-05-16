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
      title: "Trip Histories",
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
          text: "Destination",
          value: "destination",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Picked Up Area",
          value: "picked_up_area",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Fare",
          value: "fare",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Distance",
          value: "distance",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Total Passenger",
          value: "total_passenger",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Driver Id",
          value: "driver_id",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Passenger Id",
          value: "passenger_id",
          filterable:true,
          sortType:null,
          filterValue:''
        },
        {
          text: "Vehicle Id",
          value: "vehicle",
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
      this.$axios.get(`histories`).then(({data}) => {
        this.data = data.data
        this.options = data.options
      })
    },
    getUsers(){
      this.$axios.get(`histories`).then(({data}) => {
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
      this.$root.dialog(
        "Confirm Action!",
        `Are you sure you want to delete ${items.length == 1 ? 'this record' : 'these records'} ?`,
        "delete"
      ).then(() => {
        let ids = this.getIds(items)
        this.$axios.delete(`${this.$histories}/${ids}`).then(({data}) => {
          this.successNotification(items, 'deleted', 'users', 'users')
          this.initialize()
        })
      });
    },
  },
};
</script>

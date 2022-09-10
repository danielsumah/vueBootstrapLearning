<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <b-button @click="toggleBusy">Toggle Busy State</b-button>
    <div>
        <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        limit="3"
        aria-controls="my-table"
         ></b-pagination>

      <p class="mt-3">Current Page: {{ currentPage }}</p>
        
      <b-table :per-page="perPage" :current-page="currentPage" hover :items="items" :busy="isBusy" ></b-table>
        <!-- <template #table-busy>
        <div class="text-center text-danger my-2">
          <b-spinner class="align-middle"></b-spinner>
          <strong>Loading...</strong>
        </div>
      </template> -->
  </div>

  <div>
    <b-table stacked striped hover :items="items2" :fields="fields2"></b-table>
  </div>

  <div>
    <b-table dark striped hover :items="items3" :fields="fields3"></b-table>
  </div>

  <div>
    <b-table :items="items4" :fields="fields4" striped responsive="sm">
      <template #cell(show_details)="row">
        <b-button size="sm" @click="row.toggleDetails" class="mr-2">
          {{ row.detailsShowing ? 'Hide' : 'Show'}} Details
        </b-button>

        <!-- As `row.showDetails` is one-way, we call the toggleDetails function on @change -->
        <b-form-checkbox v-model="row.detailsShowing" @change="row.toggleDetails">
          Details via check
        </b-form-checkbox>
      </template>

      <template #row-details="row">
        <b-card>
          <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>Age:</b></b-col>
            <b-col>{{ row.item.age }}</b-col>
          </b-row>

          <b-row class="mb-2">
            <b-col sm="3" class="text-sm-right"><b>Is Active:</b></b-col>
            <b-col>{{ row.item.isActive }}</b-col>
          </b-row>

          <b-button size="sm" @click="row.toggleDetails">Hide Details</b-button>
        </b-card>
      </template>
    </b-table>
  </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  computed: {
      rows() {
        return this.items.length
      }
    },
  data() {
      return {
        perPage: 3,
        currentPage: 1,
        isBusy: false,
        items: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw',_cellVariants: { age: 'info', first_name: 'warning' } },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' ,_showDetails: true},
          { age: 38, first_name: 'Jami', last_name: 'Carney' ,_rowVariant: 'danger'},
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw',_cellVariants: { age: 'info', first_name: 'warning' } },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' ,_showDetails: true},
          { age: 38, first_name: 'Jami', last_name: 'Carney' ,_rowVariant: 'danger'},
          { age: 21, first_name: 'Larsen', last_name: 'Shaw',_cellVariants: { age: 'info', first_name: 'warning' } },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' ,_showDetails: true},
          { age: 38, first_name: 'Jami', last_name: 'Carney' ,_rowVariant: 'danger'},
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw',_cellVariants: { age: 'info', first_name: 'warning' } },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' ,_showDetails: true},
          { age: 38, first_name: 'Jami', last_name: 'Carney' ,_rowVariant: 'danger'}
        ],

        fields2: ['first_name', 'last_name', 'age'],
        items2: [
          { isActive: true, age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { isActive: true, age: 38, first_name: 'Jami', last_name: 'Carney' }
        ],

        // Note 'isActive' is left out and will not appear in the rendered table
        fields3: [
          {
            key: 'last_name',
            sortable: true
          },
          {
            key: 'first_name',
            sortable: false
          },
          {
            key: 'age',
            label: 'Person age',
            sortable: true,
            // Variant applies to the whole column, including the header and footer
            variant: 'danger'
          }
        ],
        items3: [
          { isActive: true, age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { isActive: true, age: 38, first_name: 'Jami', last_name: 'Carney' }
        ],


        fields4: ['first_name', 'last_name', 'show_details'],
        items4: [
          { isActive: true, age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          {
            isActive: false,
            age: 89,
            first_name: 'Geneva',
            last_name: 'Wilson',
            _showDetails: true
          },
          { isActive: true, age: 38, first_name: 'Jami', last_name: 'Carney' }
        ]

      }
    },
    methods: {
      toggleBusy() {
        this.isBusy = !this.isBusy
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

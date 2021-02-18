<!-- @format -->

<template>
  <div class="container" id="app">
    <div class="row">
      <div class="two columns"></div>
      <div class="eight columns">
        <h1>Vue CSV</h1>

        <h2>Example Template</h2>
        <p>
          You can download <a href="/fleet.csv">this template</a> for your
          convenience.
        </p>
        <form @submit.prevent="onSubmit">
          <vue-csv-import
            :headers="[
              'Vehicle Make',
              'Vehicle Model',
              'Year Of Make',
              'Registration Number',
              'Engine Number',
              'Chassis Number',
              'Color',
              'Cubic Capacity',
              'Seating Capacity',
              'Body Type',
              'Certificate Number',
              'Vehicle Class',
            ]"
            :map-fields="{
              vehicleMake: 'Vehicle Make',
              vehicleModel: 'Vehicle Model',
              yearOfManufacture: 'Year Of Make',
              regNumber: 'Registration Number',
              engineNumber: 'Engine Number',
              chassisNumber: 'Chassis Number',
              color: 'Color',
              cubicCapacity: 'Cubic Capacity',
              seatingCapacity: 'Seating Capacity',
              bodyType: 'Body Type',
              certificateNumber: 'Certificate Number',
              productType: 'Vehicle Class',
            }"
            :can-ignore="false"
            :file-mime-types="['text/csv']"
            auto-match-fields
            auto-match-ignore-case
            table-class="u-full-width"
            v-model="csv"
          >
            <template slot="next" slot-scope="{ load }">
              <div class="d-flex justify-content-end">
                <button @click.prevent="load" v-if="!csv.length > 0">
                  Load File
                </button>
              </div>
            </template>
          </vue-csv-import>
          <table class="u-full-width">
            <thead>
              <tr>
                <th>Vehicle Make</th>
                <th>Vehicle Model</th>
                <th>Year Of Make</th>
                <th>Registration Number</th>
                <th>Engine Number</th>
                <th>Chassis Number</th>
                <th>Color</th>
                <th>Cubic Capacity</th>
                <th>Seating Capacity</th>
                <th>Body Type</th>
                <th>Certificate Number</th>
                <th>Vehicle Class</th>
              </tr>
            </thead>
            <tbody>
              <tr :key="index" v-for="(item, index) in csv">
                <td>{{ item.vehicleMake }}</td>
                <td>{{ item.vehicleModel }}</td>
                <td>{{ item.yearOfManufacture }}</td>
                <td>{{ item.regNumber }}</td>
                <td>{{ item.engineNumber }}</td>
                <td>{{ item.chassisNumber }}</td>
                <td>{{ item.color }}</td>
                <td>{{ item.cubicCapacity }}</td>
                <td>{{ item.seatingCapacity }}</td>
                <td>{{ item.bodyType }}</td>
                <td>{{ item.certificateNumber }}</td>
                <td>{{ item.productType }}</td>
              </tr>
            </tbody>
          </table>

          <button type="submit">Submit CSV</button>
        </form>

        <!-- <pre><code>CSV: {{ csv }}</code></pre> -->
      </div>
    </div>
  </div>
</template>

<script>
  import { VueCsvImport } from 'vue-csv-import'

  export default {
    name: 'App',
    components: {
      VueCsvImport,
    },

    data: () => ({
      csv: [],
    }),

    methods: {
      onSubmit() {
        alert(`Data entered: ${JSON.stringify(this.csv)}`)
      },
    },
  }
</script>

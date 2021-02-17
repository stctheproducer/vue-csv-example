<template>
  <div class="container" id="app">
    <div class="row">
      <div class="two columns"></div>
      <div class="eight columns">
        <h1>Vue CSV</h1>

        <h2>Example Template</h2>
        <p>You can download <a href="/example.csv">this template</a> for your convenience.</p>
        <form @submit.prevent="onSubmit">
          <!--          :map-fields="['name', 'age']"-->
          <vue-csv-import
              :headers="['Name', 'Age']"
              :map-fields="{name: 'Name', age: 'Age'}"
              :can-ignore="false"
              :file-mime-types="['text/csv']"
              auto-match-fields
              auto-match-ignore-case
              table-class="u-full-width"
              v-model="csv"
          >

            <template slot="next" slot-scope="{ load }">
              <div class="d-flex justify-content-end">
                <button
                    @click.prevent="load"
                    v-if="!csv.length > 0"
                >Load File
                </button
                >
              </div>
            </template>
          </vue-csv-import>
          <table class="u-full-width">
            <thead>
            <tr>
              <th>Name</th>
              <th>Age</th>
            </tr>
            </thead>
            <tbody>
            <tr :key="index" v-for="(person, index) in csv">
              <td>{{ person.name }}</td>
              <td>{{ person.age }}</td>
            </tr>
            </tbody>
          </table>

          <button type="submit">Submit CSV</button>
        </form>

        <pre><code>{{ csv }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script>
    import {VueCsvImport} from 'vue-csv-import'

    export default {
        name: 'App',
        components: {
            VueCsvImport
        },

        data: () => ({
            csv: []
        }),

        methods: {
            onSubmit() {
                alert(`Data entered: ${JSON.stringify(this.csv)}`)
            }
        }
    }
</script>

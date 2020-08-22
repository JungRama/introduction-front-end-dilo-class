<template>
  <v-container>
    <!-- BUTTON CREATE -->
    <v-btn color="primary" style="margin-left: 15px"
    @click="isCreate = !isCreate">+ TAMBAH DATA BARU</v-btn>

    <v-card style="padding: 20px; margin-left: 15px; margin-top: 20px;" 
      v-if="isCreate">
      <h3>Create Data</h3>
      <v-text-field
        v-model="form.username"
        label="Username"
        required>
      </v-text-field>

      <v-text-field
        v-model="form.title"
        label="Title"
        required>
      </v-text-field>

      <v-text-field
        v-model="form.body"
        label="Body"
        required>
      </v-text-field>

      <v-card-actions>
        <v-btn @click="submitForm" text>Create New Data</v-btn>
      </v-card-actions>
    </v-card>

    <!-- BUTTON CREATE -->
    <v-row>
      <v-col cols="12" sm="4" v-for="item in listData" :key="item._id">
        <!-- CARD -->
          <v-card class="mx-auto" max-width="344" outlined>
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4">{{ item.title }}</div>
                <v-list-item-title class="headline mb-1">{{ item.body }}</v-list-item-title>
                <v-list-item-subtitle>{{ item.username }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>

            <v-card-actions>
              <!-- <v-btn text>Edit</v-btn> -->
              <v-btn text @click="deleteData(item._id)">Delete</v-btn>
            </v-card-actions>
          </v-card>
        <!-- CARD -->
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        // FORM DATA
        form: {
          username: '',
          title: '',
          body: '',
        },

        listData: [],
        isCreate: false
      }
    },
    methods: {
      // LOAD DATA
      async loadData() {
        const response = await axios.get('https://fe-dilo.herokuapp.com/api/documents')
        this.listData = response.data
      },
      // SUBMIT FORM
      async submitForm() {
        await axios.post('https://fe-dilo.herokuapp.com/api/documents', {
          ...this.form
        })

        this.loadData()
      },
      // DELETE DATA
      async deleteData(id) {
        await axios.delete('https://fe-dilo.herokuapp.com/api/documents/' + id)
        this.loadData()
      }
    },
    async mounted() {
      this.loadData()
    }
  }
</script>

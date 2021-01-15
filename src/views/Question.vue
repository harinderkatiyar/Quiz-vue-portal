<template>
  <div>
    <base-header type="gradient-success" class="pb-6 pb-4 pt-5 pt-md-8">
    </base-header>

    <div class="container-fluid mt--7">
      <div class="row">
        <div class="col">
          <div class="card shadow">
            <div class="card-header bg-transparent">
              <h3 class="mb-0">View Question</h3>
            </div>
            <div class="card-body">
              <div class="row">
                <div data-app>
                  <v-dialog v-model="dialog" persistent max-width="700px">
                    <template v-slot:activator="{ on }">
                      <v-card-actions>
                        <v-btn
                          class="mx-2"
                          fab
                          dark
                          large
                          color="cyan"
                          title="Upload Question"
                        >
                          <i class="fa fa-upload fa-lg" aria-hidden="true"></i>
                        </v-btn>
                        <v-spacer></v-spacer>
                        <v-btn
                          class="mx-2"
                          fab
                          dark
                          large
                          color="cyan"
                          title="Add Question"
                          v-on="on"
                        >
                          <i class="fa fa-plus fa-lg" aria-hidden="true"></i>
                        </v-btn>
                      </v-card-actions>
                    </template>
                    <v-card>
                      <v-card-title>
                        <span v-if="editedItem.id"
                          >Edit Question {{ editedItem.id }}</span
                        >
                        <span v-else>Add Question</span>
                      </v-card-title>
                      <v-card-text>
                        <v-row>
                          <v-col cols="12" md="12">
                            <v-textarea
                              outlined
                              name="input-7-4"
                              label="Question Content"
                              rows="1"
                            ></v-textarea>
                          </v-col>
                          <v-col cols="12" md="6">
                            <v-textarea
                              outlined
                              name="input-7-4"
                              label="Answer 1"
                              rows="1"
                            ></v-textarea>
                          </v-col>
                          <v-col cols="12" md="6">
                            <v-textarea
                              outlined
                              name="input-7-4"
                              label="Answer 2"
                              rows="1"
                            ></v-textarea>
                          </v-col>
                          <v-col cols="12" md="6">
                            <v-textarea
                              outlined
                              name="input-7-4"
                              label="Answer 3"
                              rows="1"
                            ></v-textarea>
                          </v-col>
                          <v-col cols="12" md="6">
                            <v-textarea
                              outlined
                              name="input-7-4"
                              label="Answer 4"
                              rows="1"
                            ></v-textarea>
                          </v-col>
                          <v-col cols="12" md="12">
                            <v-textarea
                              outlined
                              name="input-7-4"
                              label="Correct Answer"
                              rows="1"
                            ></v-textarea>
                          </v-col>
                          <v-col class="d-flex" cols="12" sm="6">
                            <v-select
                              :items="profileDropDown"
                              label="Profile"
                              item-text="value"
                              item-value="id"
                            ></v-select>
                          </v-col>
                          <v-col cols="12" sm="6">
                            <v-text-field
                              v-model="editedItem.ans2"
                              label="Catagory"
                            ></v-text-field>
                          </v-col>
                          <v-col class="d-flex" cols="12" sm="6">
                            <v-select
                              :items="difficultyDropDown"
                              label="Difficulty"
                              item-text="value"
                              item-value="id"
                            ></v-select>
                          </v-col>
                          <v-col class="d-flex" cols="12" sm="6">
                            <v-select
                              :items="multiplSelectionDropDown"
                              label="Mutiple Selection"
                              item-text="value"
                              item-value="id"
                            ></v-select>
                          </v-col>
                          <!-- <v-col cols="12" sm="8">
                                <v-text-field
                                  v-model="editedItem.ans2"
                                  label="Details"
                                ></v-text-field>
                              </v-col>
                              <v-col cols="12" sm="12">
                                <v-text-field
                                  v-model="editedItem.ans2"
                                  label="URL"
                                ></v-text-field>
                              </v-col> -->
                        </v-row>
                      </v-card-text>
                      <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn
                          color="blue darken-1"
                          text
                          @click="showEditDialog()"
                          >Cancel</v-btn
                        >
                        <v-btn
                          color="blue darken-1"
                          text
                          @click="saveItem(editedItem)"
                          >Save</v-btn
                        >
                      </v-card-actions>
                    </v-card>
                  </v-dialog>
                  <v-main class="container align-center px-1">
                    <!-- <h2 class="font-weight-light mb-2">Vuetify CRUD Example</h2> -->
                    <v-card>
                      <v-card-title>
                        Question
                        <v-spacer></v-spacer>
                        <v-text-field
                          v-model="search"
                          append-icon="mdi-magnify"
                          label="Search"
                          single-line
                          hide-details
                        ></v-text-field>
                      </v-card-title>
                      <v-data-table
                        :headers="headers"
                        :items="items"
                        :search="search"
                        mobile-breakpoint="800"
                        class="elevation-0"
                      >
                        <template v-slot:[`item.actions`]="{ item }">
                          <div class="text-truncate">
                            <button
                              small
                              class="mr-2"
                              @click="showEditDialog(item)"
                              color="primary"
                              title="Edit"
                            >
                              <i class="fa fa-edit" aria-hidden="true"></i>
                            </button>

                            <button
                              small
                              @click="deleteItem(item)"
                              color="pink"
                              title="Delete"
                            >
                              <i class="fa fa-trash" aria-hidden="true"></i>
                            </button>
                          </div>
                        </template>
                        <template v-slot:[`item.details`]="{ item }">
                          <div class="text-truncate" style="width: 180px">
                            {{ item.Details }}
                          </div>
                        </template>
                        <template v-slot:[`item.url`]="{ item }">
                          <div class="text-truncate" style="width: 180px">
                            <a :href="item.URL" target="_new">{{ item.URL }}</a>
                          </div>
                        </template>
                      </v-data-table>
                      <!-- this dialog is used for both create and update -->
                    </v-card>
                  </v-main>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import io from "../../config";
import axios from "axios";
import Vue from "vue";
import VueClipboard from "vue-clipboard2";
import BTooltipDirective from "bootstrap-vue/esm/directives/tooltip";
import Vuetify from "vuetify";
Vue.use(VueClipboard);
export default {
  
  vuetify: new Vuetify({}),
  directives: {
    "b-tooltip": BTooltipDirective,
  },
  data() {
    return {
      dataTableData: [],
      error: [],
      search: "",
      selected: "",
      addJobSeekerForm: {
        name: null,
        profile: null,
        email: null,
        mobile: null,
        experience: null,
        duration: null,
        isQuizRequired: null,
        address: null,
      },
      headers: [
        { text: "Id", value: "question_id" },
        {
          text: "Question content",
          value: "question_content",
        },
        { text: "Answer 1", value: "ans1" },
        { text: "Answer 2", value: "ans2" },
        { text: "Answer 3", value: "ans3" },
        { text: "Answer 4", value: "ans4" },
        { text: "Difficulty", value: "difficulty" },
        { text: "Category", value: "category" },
        { text: "Mutiple Selection", value: "isMutipleSelection" },
        { text: "Action", value: "actions", sortable: false },
      ],
      items: [],
      dialog: false,
      editedItem: {},
      profileDropDown: [
        { id: "ForntEnd", value: "ForntEnd" },
        { id: "Backend", value: "Backend" },
        { id: "Other", value: "Other" },
      ],
      difficultyDropDown: [
        { id: "Low", value: "Low" },
        { id: "Medium", value: "Medium" },
        { id: "Hard", value: "Hard" },
      ],
      multiplSelectionDropDown: [
        { id: "Yes", value: "Yes" },
        { id: "NO", value: "No" },
      ],
    };
  },
  methods: {
    handleAction(action, payload) {
      console.log(action, payload);
      window.alert("check out the console to see the data logged");
    },
    showEditDialog(item) {
      this.editedItem = item || {};
      this.dialog = !this.dialog;
    },
    loadItems() {
      this.items = [];
      axios
        .get(`https://api.airtable.com/v0/`, {
          headers: { Authorization: "Bearer " },
        })
        .then((response) => {
          this.items = response.data.records.map((item) => {
            return {
              id: item.id,
              ...item.fields,
            };
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
    saveItem(item) {
      /* this is used for both creating and updating API records
         the default method is POST for creating a new item */

      let method = "post";
      let url = `https://api.airtable.com/v0/`;
      let id = item.id;

      // airtable API needs the data to be placed in fields object
      let data = {
        fields: item,
      };

      if (id) {
        // if the item has an id, we're updating an existing item
        method = "patch";
        url = `https://api.airtable.com/v0/`;

        // must remove id from the data for airtable patch to work
        delete data.fields.id;
      }

      // save the record
      axios[method](url, data, {
        headers: {
          Authorization: "Bearer ",
          "Content-Type": "application/json",
        },
      }).then((response) => {
        if (response.data && response.data.id) {
          console.log(response.data);
          // add new item to state
          this.editedItem.id = response.data.id;
          if (!id) {
            // add the new item to items state
            this.items.push(this.editedItem);
          }
          this.editedItem = {};
        }
        this.dialog = !this.dialog;
      });
    },
    deleteItem(item) {
      //console.log('deleteItem', item)
      let id = item.id;
      let idx = this.items.findIndex((item) => item.id === id);
      if (confirm("Are you sure you want to delete this?")) {
        /* not really deleting in API for demo */
        /*
            axios.delete(`https://api.airtable.com/v0/${airTableApp}/${airTableName}/${id}`,
                { headers: { 
                    Authorization: "Bearer " + apiToken,
                    "Content-Type": "application/json"
                }
            }).then((response) => {
                this.items.splice(idx, 1)
            })*/
        this.items.splice(idx, 1);
      }
    },
  },
  mounted() {
    this.loadItems(),
      axios({
        method: "get",
        url: `${io.baseURL}/common/getQuestion`,
      })
        .then(
          (response) => (
            console.log("----------", response.data.data),
            (this.items = response.data.data)
          )
        )
        .catch((error) => {
          console.log(error);
        });
  },
};
</script>
<style></style>

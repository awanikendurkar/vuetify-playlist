<template>
  <v-dialog max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-btn text class="success" v-bind="attrs" v-on="on">
        Add new project
      </v-btn>
    </template>
    <v-card>
      <v-card-title>
        <h2>Add a new project</h2>
      </v-card-title>
      <v-card-text>
        <v-form class="px-3">
          <v-text-field
            label="Title"
            v-model="title"
            prepend-icon="mdi-folder"
          ></v-text-field>
          <v-textarea
            label="Information"
            v-model="content"
            prepend-icon="mdi-pencil"
          ></v-textarea>

          <v-menu
            v-model="menu2"
            :close-on-content-click="false"
            max-width="290"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                :value="computedDateFormattedDatefns"
                clearable
                label="Due date"
                readonly
                prepend-icon="mdi-calendar-range"
                v-bind="attrs"
                v-on="on"
                @click:clear="date = null"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="date"
              @change="menu2 = false"
            ></v-date-picker>
          </v-menu>

          <!-- <v-menu
            v-model="menu"
            :close-on-content-click="false"
            max-width="290"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                :value="formattedDate"
                clearable
                label="Due date"
                readonly
                prepend-icon="mdi-calendar-range"
                v-bind="attrs"
                v-on="on"
                @click:clear="due = null"
              >
              </v-text-field>
            </template>
            <v-date-picker v-model="due" @change="menu = false"></v-date-picker>
          </v-menu> -->

          <v-spacer></v-spacer>

          <v-btn text class="success mx-0 mt-3" @click="submit"
            >Add project</v-btn
          >
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import { format, parseISO } from "date-fns";
export default {
  data() {
    return {
      title: "",
      content: "",
      //   due: null, //format(parseISO(new Date().toISOString()), "yyyy-MM-dd"),
      //   menu: false,
      date: format(parseISO(new Date().toISOString()), "yyyy-MM-dd"),
      menu2: false,
    };
  },
  methods: {
    submit() {
      console.log(this.title, this.content);
    },
  },
  computed: {
    // formattedDate() {
    //   console.log(this.due);
    //   return this.due ? format(this.due, "Do MMM YYYY") : "";
    // },
    computedDateFormattedDatefns() {
      return this.date ? format(parseISO(this.date), "do MMM yyyy") : "";
    },
  },
};
</script>
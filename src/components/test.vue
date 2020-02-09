<template>
  <section>
    <div id="vantajs" style="position: absolute; z-index: 0; top: 0px; left: 0px; width: 1903px; height: 535px;" >
      <v-container fill-height fluid>
        <v-row align="center" justify="center">
          <v-flex xs4>
          </v-flex>
          <v-flex xs4>
            <form>
              <v-text-field v-model="word" label="Any Swedish words" required v-on:input="showMore(word)"></v-text-field>
            </form>
          </v-flex>
          <v-flex xs4>
          </v-flex>
        </v-row>
      </v-container>
    </div>
  </section>
</template>

<script>
import { APIService } from "../APIService";
import HelloWorld from "./HelloWorld.vue";

const API_URL = "http://localhost:8000";
const apiService = new APIService();

export default {
  name: "ListContacts",

  components: {
    HelloWorld
  },

  data() {
    return {
      contacts: [],
      numberOfContacts: 0,
      word: ''
    };
  },

  methods: {
    getContacts() {
      apiService.getContacts().then(data => {
        console.log(data);
        this.contacts = data;
        this.numberOfContacts = data.count;
        console.log("화이팅");
      });
    },
    showMore(word){
      console.log(word);
    },
 
  },

  mounted() {
    window.VANTA.CLOUDS({
      el: "#vantajs",
      mouseControls: true,
      touchControls: true,
      minHeight: 1000.0,
      minWidth: 200.0
    });

    this.getContacts();
  }
};
</script>

<style>
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: yellow;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background-color: red;
}
</style>
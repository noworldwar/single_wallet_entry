<template>
  <div class="hello">
    <table style="width: 30%">
      <tr>
        <td>
          <label class="sr-only" for="inline-form-input-playerid"
            >PID</label>
          <b-input-group prepend="玩家" class="mb-2 mr-sm-2 mb-sm-0">
            <b-form-select
              v-model="selected"
              :options="options"
            ></b-form-select>
          </b-input-group>
        </td>
      </tr>
      <tr><td></td></tr>
      <tr><td></td></tr>
      <tr><td></td></tr>
      <tr>
        <td>
          <b-button variant="primary" style="width: 100%" v-on:click="openGameHandler()">開啟遊戲</b-button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>

import axios from "../../node_modules/axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      selected: "mike",
      options: [
        { value: "mike", text: "Mike" },
        { value: "willis", text: "Willis" },
      ],
    };
  },
  methods: {
    openGameHandler() {
      openGameRequest(this.selected);
    }
  }
};

function openGameRequest(value) {
  console.log(value)
  const form = new FormData();
  form.append("playerID", value);
    axios
      .post("http://3.17.135.216:7901/validate", form)
      // .post("http://localhost/validate", form)
      .then(function (response) {
        // console.log(response)
        window.location.href = 'https://dev-web-game-fe.dvweg.com/?token='+ response.data.playerID +'&operator=agofhjg0'
      })
      .catch(function (error) {
        console.log(error)
      });
  return;
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

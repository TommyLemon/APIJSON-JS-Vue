<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div class="#show">动态内容: {{ Moment.content }}</div>
    <div class="#show">用户名: {{ User.name }}</div>
    <button @click="ok()" >{{ msg }}</button>
  </div>
</template>
<script>
  import axios from 'axios'

  // axios.defaults.withCredentials = true


  var url_base = "http://139.196.140.118:8080"
  var url_get = url_base + "/get"
  var url_head = url_base + "/head"
  var url_post_get = url_base + "/post_get"
  var url_post_head = url_base + "/post_head"
  var url_post = url_base + "/post"
  var url_put = url_base + "/put"
  var url_delete = url_base + "/delete"

  var model = {
    msg: 'APIJSON',
    Moment: {
      content:'content'
    },
    User: {
      name:'name'
    }
  }

  export default {
    name: 'app',
    data () {
      return model
    },
    methods: {
      ok() {
        // 刷新界面
        function refresh(data) {
          if (data == null) {
            data = {}
          }

          model.Moment = data.Moment == null ? {} : data.Moment
          model.User = data.User == null ? {} : data.User

          console.log('refresh  model = \n' + JSON.stringify(model))
        }

        axios.get(url_get + '/' + JSON.stringify(
        {
          Moment: {
            userId: 70793
          },
          User: {
            id: 70793
          }
        }),
        {
          params: {}
        })
        .then(function (response) {
          refresh(response.data)
        })
        .catch(function (error) {
          console.log(error);
        })

      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  h1, h2 {
    font-weight: normal;
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


  #show {
    height: 100px;
    width: 1000px;
    background-color: #000000;
    text-decoration-color: #ffffff;
  }

</style>

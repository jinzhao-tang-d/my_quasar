<template>
  <!-- <q-bar dark class="bg-primary text-white">
    <q-btn dense flat round icon="lens" size="8.5px" color="red" />
    <q-btn dense flat round icon="lens" size="8.5px" color="yellow" />
    <q-btn dense flat round icon="lens" size="8.5px" color="green" />
    <div class="col text-center text-weight-bold">
      My-App
    </div>
  </q-bar> -->
  <div id="q-app">
    <!-- <div class=""></div> -->

    <q-img
      :src="imgUrl"
      :ratio="16/9"
      spinner-color="primary"
      spinner-size="82px"
      style="height:300px;max-width:auto"
    />
    <br/>
    <div class="row-6">
      <div class="col-6">
      <q-banner class="bg-primary text-white">
            <h5>情報：{{ info }}</h5>
        <template v-slot:action>
          <q-btn flat color="white"  @click="onClick" label="Change the data" />
          <!-- <q-btn flat color="{5:white}" label="{6:Update Credit Card}" /> -->
        </template>
      </q-banner>
      </div>
      <div class="col-6">
        <q-banner inline-actions class="text-white bg-purple-8">
            <h6>ログイン状態:{{ login }}</h6>
            <h6>ユーザー名：{{user}}</h6>
          <!-- <template v-slot:action>
            <q-btn flat color="{3:white}" label="{4:Dismiss}" />
            <q-btn flat color="{5:white}" label="{6:Update Credit Card}" />
          </template> -->
        </q-banner>

      </div>
    </div>
    
  </div>
</template>
<script>
import axios from 'axios'
import qs from 'qs'
const path = "basic";
export default {
  name: "App",
  data() {
    return {
      login: "not yet",
      info: "initial",
      user: "null",
      imgUrl:""
    };
  },
  // computed: {
  //   name() {
  //     return this.data;
  //   }
  // },
  mounted() {
    const data = { 'username': 'user', 'password': 'pass' };
    axios.post(`http://localhost:8882/${path}`,
    data
    ).then(response =>(this.login=response.data.msg,this.user=response.data.username));
  },
  created () {
     axios.get("http://localhost:8882/img",{
      // headers:{
      //   "Content-Type":"image/jpeg"
      // }
    })
    .then((data)=>{
      console.log(data)
      this.imgUrl=data.data
    });
  },
  methods: {
    onClick() {
      axios
        .get("http://localhost:8881/")
        .then(response => (this.info = response.data))
        .catch(function(error) {
          console.log("wrong:", error);
        });
    }
  }
};
</script>

<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col>
        <b-card
          header="مشخصات فروشنده"
          border-variant="primary"
          class="bg-gray-100 text-center"
          col-md-4
          style="width:80%; margin-left:auto;margin-right:auto;direction:rtl"
        >
          <table
            class="table table-bordered bg-white"
            style="width:70%;margin-left:50px;direction:ltr;float:left"
          >
            <tbody>
              <tr>
                <td class="col-6" align="right">{{this.blog.name}}</td>
                <td class="col-2" align="right">نام</td>
              </tr>

              <tr>
                <td class="col-6" align="right">{{this.blog.email}}</td>
                <td class="col-2" align="right">ایمیل</td>
              </tr>
              <tr>
                <td class="col-6" align="right">{{this.blog.phoneNumber}}</td>
                <td class="col-2" align="right">تلفن همراه</td>
              </tr>
              <tr>
                <td class="col-6" align="right">{{this.blog.location}}</td>
                <td class="col-2" align="right">موقعیت</td>
              </tr>
              <tr>
                <td class="col-6" align="right">{{this.blog.activityFields}}</td>
                <td class="col-2" align="right">زمینه فعالیت</td>
              </tr>
              <tr>
                <td class="col-6" align="right">{{this.blog.activityDescription}}</td>
                <td class="col-2" align="right">توضیح فعالیت</td>
              </tr>
            </tbody>
          </table>
          <img
            style=" width:150px; height:150px; float:right; margin-right:30px"
            v-bind:src="this.blog.identificationImage"
            class="img-rounded"
            alt="identification Image"
          />
          <div class="clearfix"></div>

          <b-col>
            <b-button v-on:click="SendApprove" variant="primary" class="px-4 float-left">تایید</b-button>
          </b-col>
        </b-card>
      </b-col>
    </b-row>
    <!--/.row-->
  </div>
</template>

<script>
import { Switch as cSwitch } from "@coreui/vue";
import axios from "axios";
// const axios = require('axios').default;
export default {
  name: "cards",
  components: {
    cSwitch
  },
  data() {
    return {
      show: true,
      //username: "فروشنده شماره1",
     username:this.$route.params.userName,
      blog: "",
      cookie: "",
      t: { userName: "string", password: "string" },
      idApprove: 0
    };
  },
  created() {},
  beforeMount(){
this.Login();
  },
  methods: {
    Approve() {
      axios.defaults.headers.common["Authorization"] = "Bearer " + this.cookie;
      axios
        .post("http://198.143.182.157/api/Salesmans/GetByUserNameAsync", {
          userName: this.username
        })
        .then(response => {
          this.blog = response.data;
          this.idApprove = response.data.id;
        })
        .catch(error => {
          // handle error
          console.log(error);
        });
     // setTimeout(this.SendApprove, 5000);
    },
    SendApprove() {
      axios.defaults.headers.common["Authorization"] = "Bearer " + this.cookie;

      axios
        .post(
          "http://198.143.182.157/api/Salesmans/Approve?id=" + this.idApprove
        )
        .then(response => {
          // handle success
          console.log("success");
        })
        .catch(error => {
          // handle error
          console.log(error);
        });
    },
    Login() {
      axios
        .post("http://198.143.182.157/api/Admin/Login", this.t)
        .then(response => {
          console.log(response.data.token);
          this.cookie = response.data.token;
          this.Approve();
        })
        .catch(function(error) {
          console.log(error);
        });

      
    }
  }
};
</script>

<style scoped>
.fade-enter-active {
  transition: all 0.3s ease;
}
.fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.fade-enter,
.fade-leave-to {
  transform: translateX(10px);
  opacity: 0;
}
</style>
<template>
  <div>
    <div class="container">
      <div class="row">
        <div
          class="col-md-6 col-sm-8 col-xs-12 col-md-offset-3 col-sm-offset-2"
          style="margin:auto;padding-rigt:0%;padding-left:0%;"
        >
          <div class="card">
            <div class="image">
              <img :src="TprofileImage" width="100%" />
            </div>

            <div class="text">
              <div class="fab" @click="SetApprove">لغو</div>

              <h3 style="direction:rtl;text-align: right;">
                نام:{{ TuserName }}
              </h3>
              <h5 style="direction:rtl;text-align: right;">آیدی:{{ Tid }}</h5>
              <p
                v-if="Tsuspend"
                style="direction:rtl;text-align: right;min-width: 285px;min-height: 43.2px"
              >
                حساب کاربری موردنظر با موفقیت مسدود شد
              </p>
              <p
                v-if="Tsuspend != null && Tsuspend != true"
                style="direction:rtl;text-align: right;"
              >
                لغو حساب کاربری به معنای قطع دسترسی فروشنده به سایت می‌باشد.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      cookie: "",
      bool: true,
      Tname: null,
      TphoneNumber: null,
      Tlocation: null,
      Temail: null,
      TidentificationImage: null,
      TprofileImage: null,
      TactivityDescription: null,
      TactivityFields: null,
      TregistrationTime: "",
      Tapproved: false,
      Tsuspend: null,
      Tproducts: null,
      Tid: null,
      TuserName: "",
      Tpassword: null,
      info: {
        userName: "mohsen",
        password: "1234"
      },
      name:""
    };
  },
  beforeMount() {
    this.register();
  },
  methods: {
    register() {
      //console.log(this.$route.params.userName);

      axios
        .post("http://198.143.182.157/api/Admin/Login", this.info)
        .then(response => {
          //console.log(response);
          this.cookie = response.data.token;
          this.name=this.$route.params.userName;
          this.AccessSeller();
          
        });
      //console.log(this.cookie);
    },
    AccessSeller() {
      //console.log(this.cookie);
      axios.defaults.headers.common["Authorization"] = "Bearer " + this.cookie;
      // axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
      axios
        .post("http://198.143.182.157/api/Salesmans/GetByUserNameAsync", {
          userName:this.name
        })
        .then(res => {
          console.log(res);
          this.Tname = res.data.name;
          this.TphoneNumber = res.data.phoneNumber;
          this.Tlocation = res.data.location;
          this.Temail = res.data.email;
          this.TidentificationImage = res.data.identificationImage;
          this.TprofileImage = res.data.profileImage;
          this.TactivityDescription = res.data.activityDescription;
          this.TactivityFields = res.data.activityFields;
          this.TregistrationTime = res.data.registrationTime;
          this.Tapproved = res.data.approved;
          this.Tsuspend = res.data.suspend;
          this.Tproducts = res.data.products;
          this.Tid = res.data.id;
          this.TuserName = res.data.userName;
          this.Tpassword = res.data.password;
          // console.log(this.Tusername)
        })
        // eslint-disable-next-line no-console
        .catch(error => console.log(error));
    },
    SetApprove() {
      axios.defaults.headers.common["Authorization"] = "Bearer " + this.cookie;
      axios
        .post("http://198.143.182.157/api/Salesmans/Edit", {
          name: this.Tname,
          phoneNumber: this.TphoneNumber,
          location: this.Tlocation,
          email: this.Temail,
          identificationImage: this.TidentificationImage,
          profileImage: this.TprofileImage,
          activityDescription: this.TactivityDescription,
          activityFields: this.TactivityFields,
          registrationTime: this.TregistrationTime,
          approved: this.Tapproved,
          suspend: true,
          products: [],
          id: this.Tid,
          userName: this.TuserName,
          password: this.Tpassword
        })
        .then(response => {
          console.log(response);
          this.bool = false;
        })
        .catch(error => console.log(error));
    }
  }
};
</script>
<style>
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #404040;
  font-size: 14px;
  font-weight: 300;
  line-height: 22px;
  letter-spacing: 0.4px;
  background: #eee;
  padding-top: 30px;
}

.card {
  display: inline-block;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.15);
  margin: 20px;
  position: relative;
  margin-bottom: 50px;
  transition: all 0.2s ease-in-out;
}

.card:hover {
  /*box-shadow: 0 5px 22px 0 rgba(0,0,0,.25);*/
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
  margin-bottom: 54px;
}

.image {
  width: 376px;
  height: 325px;
  opacity: 1;
  overflow: hidden;
  transition: all 0.2s ease-in-out;
  display: block;
  margin-right: 0%;
}

.image:hover,
.card:hover .image {
  opacity: 1;
}

.text {
  background: #fff;
  padding: 20px;
  min-height: 200px;
}

.text p {
  margin-bottom: 0px;
}

.fab {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  position: absolute;
  margin-top: -50px;
  /* right: 20px; */
  box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.3);
  color: #fff;
  font-size: 25px;
  line-height: 52px;
  text-align: center;
  background: rgba(245, 7, 7);
  -webkit-transition: -webkit-transform 0.2s ease-in-out;
  transition: transform 0.2s ease-in-out;
}

.fab:hover {
  background: #549d3c;
  cursor: pointer;
  -ms-transform: rotate(90deg);
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}
</style>

<template>
  <div>
    <div class="card-deck" style="display: flex; flex-wrap: wrap;">
      <div v-for="itm in result" :key="itm.id" class="card myCard col-3">
        <img :src="itm.profileImage" class="card-img-top" alt="Profile Image">
        <div class="card-body">
          <h5 class="card-title">نام فروشنده:</h5>
          <p class="card-text">{{itm.name}}</p>
          <div class="btns">
            <div v-if="itm.approved === false" class="approve">
              <button class="btn btn-success" @click="goToApprove(itm.userName)">تایید</button>
            </div>
            <button class="btn btn-danger suspend" @click="goToSuspend(itm.userName)">لغو</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {Switch as cSwitch} from '@coreui/vue'
  import axios from "axios";

  export default {
    name: 'cards',
    components: {
      cSwitch
    },
    data: function () {
      return {
        show: true,
        result: [],
        cookie: ""
      }
    },
    beforeCreate() {
      let data = {
        userName: "mohsen",
        password: "1234"
      };
      axios.post("http://198.143.182.157/api/Admin/Login", data)
        .then(response => {
          let data2 = {
            "sortColumn": "id",
            "order": "asc",
            "take": 1000000,
            "skip": 0,
            "expressionFilters": []
          };
          axios.post("http://198.143.182.157/api/Salesmans/GetAll", data2,
            {
              'headers': {
                'Authorization': "Bearer " + response.data.token
              }
            })
            .then(response2 => {
              this.result = response2.data.items
            });
        });
    },
    methods: {
      goToApprove(username) {
        this.$router.push(
          {
            name: 'لغو حساب کاربری فروشنده ',
            params: {userName: username}
          }
        )
      },
      goToSuspend(username) {
        this.$router.push(
          {
            name: 'تایید هویت فروشنده ',
            params: {userName: username}
          }
        )
      },
    }
  }
</script>

<style scoped>

  .myCard {
    flex: 1 0 21%; /* explanation below */
    margin: 10px;
    width: 100%;
    padding-top: 10px;
    direction: rtl;
    text-align: right;
  }

  .btns {
    text-align: center;

  }

  .approve {
    display: inline;
    float: right;
  }

  .approve button {
    padding: 5px 25px;
  }

  .suspend {
    display: inline;
    float: left;
    padding: 5px 25px;
  }

</style>

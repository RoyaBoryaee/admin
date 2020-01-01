<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col>
        <b-card
          header="مشخصات فروشنده"
          border-variant="primary"
          class="bg-gray-100"
          col-md-4
          style="width:80%; margin-left:auto;margin-right:auto;direction:rtl"
        >
          <table
            class="table table-bordered table-dark"
            style="width:70%;margin-left:50px;direction:ltr;float:left"
          >
            <tbody>
              <tr>
                <td class="col-3" align="right"><span class="h3">$</span></td>
                <td class="col-6" align="right"><p >نام</p></td>
              </tr>
              <tr>
                <td class="col-6" align="right"> <span class="h3">$</span>
</td>
                <td class="col-3" align="right"><p>ایمیل</p></td>
              </tr>
                            <tr>
                <td class="col-6" align="right"><span class="h3">$</span></td>
                <td class="col-3" align="right"> <p>تلفن همراه</p></td>
              </tr>
              <tr>
                <td class="col-6" align="right"> <span class="h3">$</span></td>
                <td class="col-3" align="right"><p>موقعیت</p></td>
              </tr>
                            <tr>
                <td class="col-6" align="right"><span class="h3">$r</span></td>
                <td class="col-3" align="right"><p>زمینه فعالیت</p></td>
              </tr>
              <tr>
                <td class="col-6" align="right"><span class="h3">$</span></td>
                <td class="col-3" align="right"><p>توضیح فعالیت</p></td>
              </tr>
            </tbody>
          </table>
          <img
            style=" width:150px; height:150px; float:right; margin-right:30px"
            src="img/avatars/7.jpg"
            class="img-rounded"
            alt="Cinque Terre"
          />
          <div class="clearfix"></div>

          <b-col>
            <b-button v-click="Approve" variant="primary" class="px-4">تایید</b-button>
          </b-col>
        </b-card>
      </b-col>
    </b-row>
    <!--/.row-->
  </div>
</template>

<script>
import { Switch as cSwitch } from "@coreui/vue";

export default {
  name: "cards",
  components: {
    cSwitch
  },
  data() {
    return {
      show: true
    };
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



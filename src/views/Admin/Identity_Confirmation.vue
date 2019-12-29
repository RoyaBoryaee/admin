<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col>
        <b-card header="Card title" border-variant="primary" class="bg-gray-100"  col-md-4 style="width:80%; margin-left:auto;margin-right:auto;">
          <img style="float:left; width:150px; height:150px;" src="img/avatars/7.jpg" class="img-rounded" alt="Cinque Terre" />

          <table
            class="table bg-white"
            style="width:70%;margin-left:auto;margin-right:auto;direction:ltr"
          >
            <tbody>
              <tr>
                <td>
                  <p >Name</p>
                </td>
                <td>
                  <span class="h3">$</span>
                </td>
              </tr>
              <tr>
                <td>
                  <p>Email</p>
                </td>
                <td>
                  <span class="h3">$</span>
                </td>
              </tr>
              <tr>
                <td>
                  <p>Phone Number</p>
                </td>
                <td>
                  <span class="h3">$</span>
                </td>
              </tr>
              <tr>
                <td>
                  <p>Locatino</p>
                </td>
                <td>
                  <span class="h3">$</span>
                </td>
              </tr>
              <tr>
                <td>
                  <p>Activity field</p>
                </td>
                <td>
                  <span class="h3">$r</span>
                </td>
              </tr>
              <tr>
                <td>
                  <p>activityDescription</p>
                </td>
                <td>
                  <span class="h3">$</span>
                </td>
              </tr>
            </tbody>
          </table>
          <div class="clearfix"></div>
          <b-col>
            <b-button v-click="Approve" variant="primary" class="px-4">Approve</b-button>
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
      show: true,

    };
  },

 
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



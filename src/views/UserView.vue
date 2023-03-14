<template>
  <div>

    <div>{{ typeof userData }}</div>
    //
    <div class="row">
      <div v-for="(nasa, v) in userData" :key="v" class="col-4">
        <div class="row container text-center">
          <div class="card" style="width: 18rem">
            <div class="card-body">
              <h5 class="card-title">Nasa</h5>
              <p class="card-text">
                {{ nasa.camera.id }} <br />
                {{ nasa.camera.name }} <br />
                {{ nasa.camera.rover_id }} <br />
                {{ nasa.camera.full_name }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const userData = ref([]);
const url = ref(
  "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=pZJYMKfcX3bnSEw889g5aSvAQ5oPCTIDQnnC4QqE&fbclid=IwAR2vOX2P_Y0z_1-ktZK1qqCdmDCrgRRg4wfAE2QCrR_Mo7xdntK3rbJuvlU"
);

function LoadUser() {
  axios
    .get(url.value)
    .then((response) => {
      userData.value = response.data.photos;
    })
    .catch((err) => {
      console.log(err);
    });
}

onMounted(() => {
  LoadUser();
});
</script>

<style>
.card {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
</style>

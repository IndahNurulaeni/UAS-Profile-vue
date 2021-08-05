<template>
  <div class="home">
    <!--img alt="Vue logo" src="../assets/logo.png">-->
    <Slider />
    <hr class="my-3" />

<Cardprofiles :profiles="profiles"/>

  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import Slider from "@/components/Slider.vue";
import Cardprofiles from "@/components/Cardprofiles.vue";
import { onMounted, ref } from "vue";

export default {
  name: "Home",
  components: {
    Slider,
    Cardprofiles,
  },

  setup() {
    let profiles = ref([]);

    onMounted(() => {
      axios
        .get('http://127.0.0.1:8000/api/profiles')
        .then((Response) => {
          profiles.value = Response.data.data;
        })
        .catch((error) => {
          console.log(error);
        })
    })

    function profileDelete(id){
      axios
        .delete(`http://127.0.0.1:8000/api/profiles/${id}`)
        .then(() => {
          let z = this.profiles.map((profiles) => profiles.id).index(id);
          this.profiles.splice(z, 1);
        })
        .catch((error) => {
          console.log(error);
        });
    }

    return {
      profiles,
      profileDelete,
    };
  },
};
</script>
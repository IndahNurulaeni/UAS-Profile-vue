<template>
  <div class="home">
    <!--img alt="Vue logo" src="../assets/logo.png">-->
    <Slider />
    <hr class="my-3" />

<h5> Contact Me </h5>
<br>
<table class="table">
      <thead class="table-blue">
        <tr>
          <th scope="col">Email</th>
          <th scope="col">No Telepon</th>
          <th scope="col">Sosial Media</th>
          <th scope="col">Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(kontak, index) in kontaks" :key="index">
          <td>{{ kontak.email}}</td>
          <td>{{ kontak.no_tlp}}</td>
          <td>{{ kontak.sosmed}}</td>
          <td>
            <router-link class="btn btn-success" :to="{name:'Editkontaks', params:{id:kontak.id}} "
              >Edit</router-link
            >
            <button @click.prevent="kontakDelete(kontak.id)" class="btn btn-primary">delete</button>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import Slider from "@/components/Slider.vue";
import { onMounted, ref } from "vue";

export default {
  name: "Home",
  components: {
    Slider,
  },

  setup() {
    let kontaks = ref([]);

    onMounted(() => {
      axios
        .get('http://127.0.0.1:8000/api/kontaks')
        .then((Response) => {
          kontaks.value = Response.data.data;
        })
        .catch((error) => {
          console.log(error);
        })
    })

    function kontakDelete(id){
      axios
        .delete(`http://127.0.0.1:8000/api/kontaks/${id}`)
        .then(() => {
          let z = this.kontaks.map((kontaks) => kontaks.id).index(id);
          this.kontaks.splice(z, 1);
        })
        .catch((error) => {
          console.log(error);
        });
    }

    return {
      kontaks,
      kontakDelete,
    };
  },
};
</script>
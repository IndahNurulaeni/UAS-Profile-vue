<template>
  <div class="card shadow mt-3">
    <div class="card-body">
      <h5 class="card-title">Edit Pendidikan</h5>
      <form class="row g-3" @submit.prevent="update">
         <div class="col-md-6">
          <label for="inputEmail4" class="form-label">No</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="pendidikan.id"
          />
          <div class="alert alert-danger" v-if="validation.id">
            {{ validation.id[0] }}
          </div>
        </div>
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">Nama</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="pendidikan.nama"
          />
          <div class="alert alert-danger" v-if="validation.nama">
            {{ validation.nama[0] }}
          </div>
        </div>
         <div class="col-6">
          <label for="inputAddress" class="form-label">Tahun</label>
          <input
            type="number"
            class="form-control"
            id="inputAddress"
           v-on="pendidikan.tahun"
          />
          <div class="alert alert-danger" v-if="validation.tahun">
            {{ validation.tahun[0] }}
          </div>
        </div>

        <div class="col-12">
          <button type="submit" class="btn btn-primary">Edit</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import { onMounted, reactive, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
export default {
  setup() {
    const pendidikan = reactive({
      id: "",
      nama: "",
      tahun: "",
    });

    let pendidikans = ref([]);
    const validation = ref([]);

    const router = useRouter();

    const route = useRoute();

    onMounted(() => {
      axios
        .get(` http://127.0.0.1:8000/api/pendidikans/${route.params.id}/edit`)
        .then((Response) => {
          console.log(Response.data.data.nama);

          pendidikan.id = Response.data.data.id;
          pendidikan.nama = Response.data.data.nama;
          pendidikan.tahun = Response.data.data.tahun;
        })
        .catch((error) => {
          console.log(error.Response.data);
        });

        axios
      .get("http://127.0.0.1:8000/api/pendidikans")
      .then((response) => {
       pendidikans.value = response.data.data;
       console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
    });

    function update() {
      let id = pendidikan.id;
      let nama = pendidikan.nama;
      let tahun = pendidikan.tahun;

      axios
        .put(` http://127.0.0.1:8000/api/pendidikans/${route.params.id}`, {
          id: id,
          nama: nama,
          tahun: tahun,
        })
        .then(() => {
          router.push({
            name: "Home",
          });
        })
        .catch((error) => {
          console.log(error);
        });
    }
    return {
      pendidikan,
      validation,
      router,
      update,
      route,
      pendidikans,
    };
  },
};
</script>
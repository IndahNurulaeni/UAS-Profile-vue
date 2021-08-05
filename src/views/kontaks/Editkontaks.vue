<template>
  <div class="card shadow mt-3">
    <div class="card-body">
      <h5 class="card-title">Edit Kontak</h5>
      <form class="row g-3" @submit.prevent="update">
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">Email</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="kontak.email"
          />
          <div class="alert alert-danger" v-if="validation.email">
            {{ validation.email[0] }}
          </div>
        </div>
         <div class="col-6">
          <label for="inputAddress" class="form-label">No Telepon</label>
          <input
            type="number"
            class="form-control"
            id="inputAddress"
           v-on="kontak.no_tlp"
          />
          <div class="alert alert-danger" v-if="validation.no_tlp">
            {{ validation.no_tlp[0] }}
          </div>
        </div>
        <div class="col-6">
          <label for="inputAddress" class="form-label">Sosial Media</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
           v-on="kontak.sosmed"
          />
          <div class="alert alert-danger" v-if="validation.sosmed">
            {{ validation.sosmed[0] }}
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
    const kontak = reactive({
      email: "",
      no_tlp: "",
      sosmed: "",
    });

    let kontaks = ref([]);
    const validation = ref([]);

    const router = useRouter();

    const route = useRoute();

    onMounted(() => {
      axios
        .get(` http://127.0.0.1:8000/api/kontaks/${route.params.id}/edit`)
        .then((Response) => {
          console.log(Response.data.data.nama);

          kontak.email = Response.data.data.email;
          kontak.no_tlp = Response.data.data.no_tlp;
          kontak.sosmed = Response.data.data.sosmed;
        })
        .catch((error) => {
          console.log(error.Response.data);
        });

        axios
      .get("http://127.0.0.1:8000/api/kontaks")
      .then((response) => {
       kontaks.value = response.data.data;
       console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
    });

    function update() {
      let email = kontak.email;
      let no_tlp = kontak.no_tlp;
      let sosmed = kontak.sosmed;

      axios
        .put(` http://127.0.0.1:8000/api/kontaks/${route.params.id}`, {
          email: email,
          no_tlp: no_tlp,
          sosmed: sosmed,
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
      kontak,
      validation,
      router,
      update,
      route,
      kontaks,
    };
  },
};
</script>
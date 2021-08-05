<template>
  <div class="row">
    <div class="col-lg-4 mt-3" v-for="(profile, index) in profiles" :key="index">
      <div class="card-header">Profile
        </div>
        <div class="card">
        <div class="card-body">
          <h5 class="card-text">{{ profile.nama }}</h5>
          <p class="card-text">{{ profile.tgl }}</p>
          <p class="card-text">{{ profile.jenis }}</p>
          <p class="card-text">{{ profile.alamat }}</p>
          <p class="card-text">{{ profile.no_tlp }}</p>
          <p class="card-text">{{ profile.email }}</p>
        </div>
        <div class="card-footer text-muted">
          <center> <router-link
            class="btn btn-primary"
            :to="{ name: 'Editprofiles', params: { id: profile.id } }"
            >Edit</router-link
          >
      <button
              @click.prevent="pendidikanDelete(pendidikan.id)"
              class="btn btn-danger"
            >
              Delete
            </button>
            </center>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["profiles"],
};
</script>

<style>
</style>
<template>
<div class="row">
  <div class="col-lg-4 mt-3" 
  v-for="(pendidikan, index) in pendidikans" :key="index">
  <div class="card-header">History Pendidikan
  </div>
  <div class="card">
  <div class="card-body">
    <h5 class="card-title">{{pendidikan.nama}}</h5>
    <p class="card-text">{{pendidikan.tahun}}</p>
    
  </div>
  <div class="card-footer text-muted">
   <center> <router-link
              class="btn btn-success"
              :to="{ name: 'Editpendidikans', params: { id: pendidikan.id } }"
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
    props: ["pendidikans"],
}
</script>

<style>

</style>
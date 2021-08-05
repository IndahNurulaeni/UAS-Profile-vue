<template>
<div class="row">
  <div class="col-lg-4 mt-3" 
  v-for="(work, index) in works" :key="index">
  <div class="card-header">work
  </div>
  <div class="card">
  <div class="card-body">
    <h5 class="card-title">{{work.posisi}}</h5>
    <h5 class="card-title">{{work.nama}}</h5>
    <p class="card-text">{{work.tahun}}</p>
    
  </div>
  <div class="card-footer text-muted">
   <center> <router-link
              class="btn btn-success"
              :to="{ name: 'Editworks', params: { id: work.id } }"
              >Edit</router-link
            >
            <button
              @click.prevent="workDelete(work.id)"
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
    props: ["works"],
}
</script>

<style>

</style>
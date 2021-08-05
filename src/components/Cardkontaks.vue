<template>
<div class="row">
  <div class="col-lg-4 mt-3" 
  v-for="(kontak, index) in kontaks" :key="index">
  <div class="card-header">Kontak
  </div>
  <div class="card">
  <div class="card-body">
    <h5 class="card-title">{{kontak.email}}</h5>
    <p class="card-text">{{kontak.no_tlp}}</p>
    
  </div>
  <div class="card-footer text-muted">
   <center> <router-link
              class="btn btn-success"
              :to="{ name: 'Editkontaks', params: { id: kontak.id } }"
              >Edit</router-link
            >
            <button
              @click.prevent="kontakDelete(kontak.id)"
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
    props: ["kontaks"],
}
</script>

<style>

</style>
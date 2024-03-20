<template>
  <div class="contsinaer-fluid">
    <div class="row">
      <div class="col-lg-12 p-5">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <input type="search" class="form-control form-cntrol-lg rounded-4" placeholder="Filter">
        </div>
        <div class="my-3 text-muted">Menampilkan 1 dari 1</div>
        <table class="table table-bordered">
          <thead>
            <tr>
              <td>NO</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.created_at }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      </div>
    <nuxt-link to="/pengunjung/tambah">
      <button type="submit" class="btn ms-3 btn-lg">KEMBALI</button>
    </nuxt-link>
  </div>
</template>

<style scoped>
button {
  border: 1px solid #000;
  background-color: #265CB5;
  color: #fff;
  position: fixed;
  bottom: 30px;
  right: 30px;
  border-radius: 20px;
}

button:hover {
  border: 1px solid #000;
  background-color: #fff;
  color: #265CB5;
}
</style>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

const getPengunjung = async () => {
  const {data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
  if(data) visitors.value = data
}

onMounted (() => {
  getPengunjung()
})

</script>
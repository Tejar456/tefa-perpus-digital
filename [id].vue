<template>

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pengunjung</title>
  </head>
  <html lang="en">

  <div class="container">
    <div v-if="loading">
      <span class="loader"></span>
      <h5 class="loading-text">Sedang memuat</h5>
    </div>

    <div v-else>
      <div class="row mt-5">
        <div class="col-md-3 card">
          <img :src="buku.cover" alt="cover">
        </div>
        <div class="p-5 col-md-9">
          <div class="badge">{{ buku.kategori }}</div>

          <ul class="text">
            <li class="list-group-item">Judul: {{ buku.judul }}</li>
            <li class="list-group-item">Penulis: {{ buku.penulis }}</li>
            <li class="list-group-item">Penerbit: {{ buku.penerbit }}</li>
            <li class="list-group-item">Tahun Penerbit: {{ buku.tahun_penerbit }}</li>
            <li class="list-group-item">Kategori: {{ buku.kategori.nama }}</li>
            <li class="list-group-item">Rak: {{ buku.rak.kode }}</li>
            <li class="list-group-item">Deskripsi: {{ buku.deskripsi }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
  <nuxt-link to="../buku">
    <button type="submit" class="btn ms-3 btn-lg">KEMBALI</button>
  </nuxt-link>

  </html>
</template>

<script setup>
const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref([])
const loading = ref(true)

const getBookById = async () => {
  loading.value = true
  const { data, error } = await supabase.from('buku').select(`*, kategori(*), rak(*)`)
    .eq('id', route.params.id)
  if (data) {
    buku.value = data[0]
    loading.value = false
  }
}

onMounted(() => {
  getBookById()
})
</script>

<style scoped>
.text {
  font-size: 1rem;
  line-height: 25px;
}

.card {
  border: none;
}

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

.loader {
  width: 48px;
  height: 48px;
  border: 5px solid #FFF;
  border-bottom-color: #008cff;
  border-radius: 50%;
  box-sizing: border-box;
  display: flex;
  margin: auto;
  align-items: center;
  margin-top: 100px;
  animation: rotation 1s linear infinite;
}

.loading-text {
  text-align: center;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
</style>

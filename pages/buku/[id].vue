<template>
    <div class="container">
    <div class="row mt-5">
        <div class="col-md-3 card">
            <img :src="buku.cover">
        </div>
        <div class="p-5 col-md-9">
            <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
            <ul class="text">
                <li class="list-group-item">Judul: {{ buku.judul }}</li>
                <li class="list-group-item">Penulis: {{ buku.penulis }}</li>
                <li class="list-group-item">Penerbit: {{ buku.penerbit }}</li> 
                <li class="list-group-item">Tahun Penerbit: {{ buku.tahun_penerbit }}</li> 
                <li class="list-group-item">Deskripsi: {{ buku.deskripsi }}</li> 
            </ul>
        </div>
    </div>
</div>
<nuxt-link to="/buku/">
    <button type="submit" class="btn ms-3 btn-lg">KEMBALI</button>
  </nuxt-link>
</template>

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
</style>

<script setup>
const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref([])

const getBookById = async () => {
    const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
    .eq('id', route.params.id)
    if(data) buku.value = data[0]
}

onMounted(() =>{
    getBookById()
})
</script>
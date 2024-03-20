<template>
    <h2 class="text-star my-4">{{ buku.judul }}</h2>
    <div class="row">
        <div class="col-md-3">
            <img :src="buku.cover">
        </div>
        <div class="col-md-6">
            <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
            <ul class="list-group list-group-flush">
                <li class="list-group-item">Penulis: {{ buku.penulis }}</li>
                <li class="list-group-item">Penulis: {{ buku.penerbit }}</li>
                <li class="list-group-item">Penulis: {{ buku.deskripsi }}</li>
            </ul>
        </div>
    </div>
</template>

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
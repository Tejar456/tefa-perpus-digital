<template>
<div>
    <div class="container">
        <div class="mb-3">
            <h1>Tambah Buku</h1>
        </div>


            <form @submit.prevent="tambahBuku">
                <div class="mb-3">
                <input
                v-model="form.judul"
                type="text"
                class="form-control form-control-lg radius"
                placeholder="Judul"
                />
            </div>
            <div class="mb-3">
                <input
                v-model="form.penulis"
                type="text"
                class="form-control form-control-lg radius"
                placeholder="Penulis"
                />
            </div>
            <div class="mb-3">
                <input
                v-model="form.deskripsi"
                type="text"
                class="form-control form-control-lg radius"
                placeholder="Deskripsi"
                />
            </div>
            <div class="mb-3">
                <input
                v-model="form.tahun_terbit"
                type="number"
                class="form-control form-control-lg radius"
                placeholder="Tahun Terbit"
                />
            </div>
            <div class="mb-3">
                <input
                v-model="form.penerbit"
                type="text"
                class="form-control form-control-lg radius"
                placeholder="Penerbit"
                />
            </div>
            <div class="mb-3">
                <input
                v-model="form.cover"
                type="text"
                class="form-control form-control-lg radius"
                placeholder="Cover"
                />
            </div>
            <div class="mb-3">
            <select
              v-model="form.kategori"
              class="form-control form-control-lg form-select radius"
            >
              <option value="" selected>KATEGORI</option>
              <option v-for="(kat, i) in kategori" :key="i" :value="kat.id">
                {{ kat.nama }}
              </option>
            </select>
          </div>
            <div class="mb-3">
            <select
              v-model="form.rak"
              class="form-control form-control-lg form-select radius"
            >
              <option value="" selected>RAK</option>
              <option v-for="(Rak, i) in noRak" :key="i" :value="Rak.id">
                {{ Rak.kode }}
              </option>
            </select>
          </div>
            <button type="submit" class="btn btn-lg radius" formaction="">
                KIRIM
            </button>
        </form>
        <NuxtLink to="/logout">
            <button type="submit" class="btn btn-lg radius logout"  formaction="">
                LOGOUT
            </button>
        </NuxtLink>
        </div>
    </div>
</template>

<script setup>
definePageMeta({
  middleware: "auth",
});

const supabase = useSupabaseClient()

const kategori = ref([])
const noRak = ref([])
const form = ref({
judul:"",
penulis:"",
deskripsi:"",
tahun_terbit:"",
penerbit:"",
cover:"",
kategori:"",
rak:"",
})

const tambahBuku = async() => {
    console.log(form.value)
    const { data , error } = await supabase.from('buku').insert([form.value]) 
}

const getKeanggotaan = async () => {
  const { data, error } = await supabase.from("kategori").select("*");
  if (data) kategori.value = data;
};

const getRak = async () => {
  const { data, error } = await supabase.from("rak").select("*");
  if (data) noRak.value = data;
};

onMounted(() => {
    getKeanggotaan()
    getRak()
})
</script>

<style scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
    flex-direction: column;
}

form {
    width: 100%;
}


button {
  border: 1px solid #000;
  background-color: #265cb5;
  color: #fff;
}

button:hover {
  border: 1px solid #000;
  background-color: #fff;
  color: #265cb5;
}

.logout {
  position: absolute;
  bottom: 20px;
  right: 20px;
}

</style>
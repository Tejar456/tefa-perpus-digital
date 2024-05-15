<template>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pengunjung</title>
  </head>
  <html lang="en">
    <div class="contsinaer-fluid">
      <div class="row">
        <div class="col-lg-12 p-5">
          <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
          <form @submit.prevent="cariPengunjung">
            <div class="my-3">
              <input
              v-model="keyword"
              type="search"
              class="form-control rounded-5"
              placeholder="Mau baca apa hari ini?"
              />
            </div>
          </form>
          <div class="my-3 text-muted">
          Menampilkan {{ visitors.length }} dari {{ visitor }}
        </div>
        <table class="table table-bordered">
          <thead>
            <tr>
              <td>NO</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>KELAS</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitors" :key="i">
              <td>{{ i + 1 }}.</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.anggota }}</td>
              <td v-if="visitor.tingkat && visitor.jurusan && visitor.kelas">{{ visitor.tingkat }} {{ visitor.jurusan}} {{ visitor.kelas }}</td>
              <td v-else>-</td>
              <td>{{ visitor.waktu }} {{ visitor.date }}</td>
              <td>{{ visitor.perlu }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <nuxt-link to="/pengunjung/tambah">
      <button type="submit" class="btn ms-3 btn-lg kembali">KEMBALI</button>
    </nuxt-link>
  </div>
  </html>
</template>

<script setup>
const supabase = useSupabaseClient();

const visitors = ref([]);
const visitor = ref(0);
const keyword = ref("");


const getPengunjung = async () => {
  const { data, error } = await supabase
  .from("semuapengunjung")
  .select()
  .order("id", { ascending: false });
  if (data) visitors.value = data;
};

const countVisitor = async () => {
  const { data, count } = await supabase
    .from("pengunjung")
    .select("*", { count: "exact" });
  if (data) visitor.value = count;
};

const cariPengunjung = async () => {
  const { data, error } = await supabase
  .from("pengunjung")
  .select(`*, keanggotaan(*), keperluan(*)`)
  .ilike("nama", `%${keyword.value}%`);
  if (data) visitors.value = data;
};


onMounted(() => {
  getPengunjung();
  countVisitor();
});
</script>

<style scoped>
button {
  border: 1px solid #000;
  background-color: #265cb5;
  color: #fff;
}

.kembali {
  position: fixed;
  bottom: 30px;
  right: 30px;
  border-radius: 20px;
}

button:hover {
  border: 1px solid #000;
  background-color: #fff;
  color: #265cb5;
}

@media only screen and (max-width: 40em) {
.table {
  font-size: 50%;
}

}
</style>

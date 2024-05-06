<template>
  <div class="contsinaer-fluid">
    <div class="row">
      <div class="col-lg-12 p-5">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <form @submit.prevent="getPengunjung">
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
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitors" :key="i">
              <td>{{ visitor.id }}.</td>
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

<script setup>
const supabase = useSupabaseClient();

const visitors = ref([]);
const visitor = ref(0);
const keyword = ref("");

const getPengunjung = async () => {
  const { data, error } = await supabase
    .from("pengunjung")
    .select(`*, keanggotaan(*), keperluan(*)`)
    // .order("id", { ascending: false });
    .ilike("nama", `%${keyword.value}%`);
  if (data) visitors.value = data;
};

const countVisitor = async () => {
  const { data, count } = await supabase
    .from("pengunjung")
    .select("*", { count: "exact" });
  if (data) visitor.value = count;
};

// const cariPengunjung = async () => {
//   const { data } = await supabase
//     .form("pengunjung")
//     .select(`*, keanggotaan(*), keperluan(*)`)
//     .ilike("nama", `%${keyword.value}%`);
//   if (data) visitors.value = data;
// };

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
</style>

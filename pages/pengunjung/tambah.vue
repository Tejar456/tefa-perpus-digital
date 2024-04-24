<template>
  <div class="container-fluid p-5">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">ISI BUKU KUNJUNGAN</h2>
        <form @submit.prevent="kirimData">
          <div class="mb-3">
            <input
              v-model="form.nama"
              type="text"
              class="form-control form-control-lg radius"
              placeholder="NAMA"
            />
          </div>
          <div class="mb-3">
            <select
              v-model="form.keanggotaan"
              class="form-control form-control-lg form-select radius"
            >
              <option value="">KEANGGOTAAN</option>
              <option
                v-for="(member, i) in members"
                :key="i"
                :value="member.id"
              >
                {{ member.nama }}
              </option>
              <!-- <option value="Siswa">Siswa</option>
              <option value="Guru">Guru</option>
              <option value="Staf">Staf</option>
              <option value="Umum">Umum</option> -->
            </select>
          </div>
          <div class="mb-3" v-if="form.keanggotaan === 6">
            <div class="row">
              <div class="col-md-4">
                <select
                  v-model="form.tingkat"
                  class="form-control form-control-lg form-select radius mb-2"
                >
                  <option value="">TINGKAT</option>
                  <option value="X">X</option>
                  <option value="XI">XI</option>
                  <option value="XII">XII</option>
                </select>
              </div>
              <div class="col-md-4">
                <select
                  v-model="form.jurusan"
                  class="form-control form-control-lg form-select radius mb-2"
                >
                  <option value="">JURUSAN</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TJKT">TJKT</option>
                  <option value="TSM">TSM</option>
                  <option value="DKV">DKV</option>
                  <option value="TOI">TOI</option>
                </select>
              </div>
              <div class="col-md-4">
                <select
                  v-model="form.kelas"
                  class="form-control form-control-lg form-select radius mb-2"
                >
                  <option value="">KELAS</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
          </div>
          <div class="mb-3">
            <select
              v-model="form.keperluan"
              class="form-control form-control-lg form-select radius"
            >
              <option value="">KEPERLUAN</option>
              <option v-for="(item, i) in objectives" :key="i" :value="item.id">
                {{ item.nama }}
              </option>
              <!-- <option value="Baca Buku">Baca Buku</option>
              <option value="Pinjam Buku">Pinjam Buku</option>
              <option value="StaKembalikan Bukuf">Kembalikan Buku</option> -->
            </select>
          </div>
          <div class="tombol">
            <button type="submit" class="btn btn-lg radius" formaction="">
              KIRIM
            </button>
            <nuxt-link to="/">
              <button type="submit" class="btn btn-lg radius kembali">
                KEMBALI
              </button>
            </nuxt-link>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.radius {
  border-radius: 20px;
}

input {
  border: 1px solid #000;
  height: 42px;
}

select {
  border: 1px solid #000;
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

.kembali {
  position: fixed;
  bottom: 30px;
  right: 30px;
  border-radius: 20px;
}
</style>

<script setup>
const supabase = useSupabaseClient();

const members = ref([]);
const objectives = ref([]);

const form = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: "",
});

const kirimData = async () => {
  // console.log(form.value)
  const { error } = await supabase.from("pengunjung").insert([form.value]);
  if (!error) navigateTo("/pengunjung");
};

const getKeanggotan = async () => {
  const { data, error } = await supabase.from("keanggotaan").select("*");
  if (data) members.value = data;
};

const getKeperluan = async () => {
  const { data, error } = await supabase.from("keperluan").select("*");
  if (data) objectives.value = data;
};

onMounted(() => {
  getKeanggotan();
  getKeperluan();
});
</script>

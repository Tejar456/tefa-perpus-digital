<template>
  <div class="container-fluid font">
    <div class="row my-5 d-flex justify-content-around">
      <div class="col-sm-5 mb-3 kartu">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-pengunjung rounded-5">
            <div class="card-body">
              <h4>Pengunjung</h4>
            </div>
          </div>
        </nuxt-link>
      </div>
      <div class="col-sm-5 kartu">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-5">
            <div class="card-body">
              <h4>Cari Buku</h4>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
    <div class="statistik">
      <h1>STATISTIK</h1>
    </div>
    <div class="row my-5 d-flex justify-content-around">
      <div class="col-sm-5 mb-3 kartu">
        <div class="card c2 rounded-5">
          <div class="card-body text">
            <h1 class="no">3</h1>
            <h3 class="pt-4">{{ visitor }}</h3>
          </div>
        </div>
      </div>
      <div class="col-sm-5 kartu">
        <div class="card c2 rounded-5">
          <div class="card-body text">
            <h1 class="no">180</h1>
            <h3 class="pt-4">{{ book }}</h3>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <chart-statistik />
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: "Home / Perpus Digital" })

const visitor = ref(0)
const book = ref(0)
  
const countVisitor = async () => {
const { data, count } = await supabase
.from('pengunjung')
.select('*', { count: 'exact' })
if(data) visitor.value = count
}

const countBook = async () => {
const { data, count } = await supabase
.from('buku')
.select('*', { count: 'exact' })
if(data) book.value = count
}

onMounted(() => {
  countVisitor()
  countBook()
)}
</script>

<style scoped>
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #17161633;
}

.card.bg-pengunjung {
  background-image: url('../assets/img/bg-home-kunjungan.jpeg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

.card.bg-buku {
  background-image: url('../assets/img/bg-home-cari-buku.jpg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

.card-body>h4 {
  color: #fff;
  position: absolute;
  bottom: 5px;
  right: 15px;
}

.statistik {
  margin-left: 100px;
}

/* .kartu {
  width: 40%;
} */

.c2 {
  border: 1px solid #000;
}

.text {
  display: flex;
  justify-content: center;
  align-items: center;
}

.no {
  font-size: 70px;
}
</style>


<template>
  <div class="row m-5">
    <div class="p-5 col-md-3 card">
      <img src="~/assets/img/cover1.jpg" class="cover">
    </div>
    <div class="p-5 col-md-9 card">
      <p>Judul : Ayah</p>
      <p>Penulis : Adrea Hirata</p>
      <p>Penerbit: PT Bentang Pustaka</p>
      <p>Tahun terbit: 2015</p>
      <p>Sinopsis : Novel Ayah menceritakan tentang persahabatan antara tiga orang kawan, yakni Sabari, Ukun, dan Tamat. Persahabatan antar ketiganya telah cukup lama, dimulai sejak duduk di bangku sekolah dasar. Namun, ada satu hal yang membedakan di antara mereka, yakni cara mendekati wanita.</p>
    </div>
  </div>
  <nuxt-link to="/buku/">
    <button type="submit" class="btn ms-3 btn-lg">KEMBALI</button>
  </nuxt-link>
</template>

<style scoped>
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


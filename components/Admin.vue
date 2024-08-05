<template>
  <div class="header">
    <div class="h-img">
      <img src="~/assets/img/LOGO-SMK4.webp" alt="logo" />
    </div>
    <div class="h-text">
      <div class="t-judul">
        <p>PERPUS DIGITAL</p>
        <p>SMK NEGERI 4 TASIKMALAYA</p>
      </div>
      <p>Jl.Depok, Sukamenak, Purbaratu 46196</p>
    </div>
  </div>
  <NuxtLink to="/logout">
    <button type="submit" class="btn btn-lg radius logout" formaction="">LOGOUT</button>
  </NuxtLink>
</template>


<style scoped>
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
.header {
  display: flex;
  align-items: center;
  width: 100%;
  height: 150px;
  background-color: #265cb5;
  color: #fff;
}

.h-img {
  margin-left: 25px;
}

.h-img > img {
  width: 80%;
}

.h-text {
  margin-left: -15px;
  line-height: 10px;
}

.t-judul {
  font-size: 20px;
  font-weight: 500;
}
@media only screen and (max-width: 40em) {
  .h-img {
    margin-left: 0.8rem;
  }

  .h-img > img {
    width: 70%;
  }

  .h-text {
    margin-left: -1.5rem;
    line-height: 5px;
  }

  .t-judul {
    font-size: 15px;
    font-weight: 500;
  }
}
</style>

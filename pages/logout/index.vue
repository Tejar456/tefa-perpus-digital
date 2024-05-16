<template>
  <div>
    <h1 class="logout">Logout</h1>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();

async function keluar() {
  const { error } = await supabase.auth.signOut();
  if (!error) navigateTo("/");
}

onMounted(() => {
  keluar()
})
</script>

<style scoped>
.logout {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
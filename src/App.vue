<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-primary">
      <div class="container">
        <a class="navbar-brand" href="#">Reddit</a>
      </div>
    </nav>
    <div class="bg-light">
      <div class="container">
        <p class="text-secondary py-1">/r/xbox</p>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

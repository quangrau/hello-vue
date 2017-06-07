<template>
  <nav class="header navbar navbar-light bg-faded">
    <router-link to="/">
      <img src="../assets/logo.png" width="30" height="30" alt="">
    </router-link>
    <ul class="header__ul navbar-nav">
        <li class="nav-item active">
            <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">Features</a>
        </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'navbar',
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  display: flex !important;
  flex-direction: row;
  align-items: center;
  width: 100%;
}
.header__ul {
  flex-direction: row;
}
.header__ul .nav-item {
  padding-left: .5rem;
  padding-right: .5rem;
}
</style>

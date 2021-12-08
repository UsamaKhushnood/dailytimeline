<template>
  <div id="app" class="container-fluid">
    <div id="nav" class="p-1 mb-5">
      <div class="row m-0">
        <div class="col-md-7 d-flex align-items-center">
          <router-link to="/" class="text-decoration-none">
            <img src="@/assets/logo.png" id="logo" />
            <!-- <h1 class="text-body">Daily Timeline</h1> -->
          </router-link>
        </div>
        <div class="col-md-5 d-flex align-items-center">
          <div class="ml-auto">
            <b-avatar></b-avatar>
          </div>
        </div>
      </div>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss" scoped>
#logo {
  width: 300px;
  filter: brightness(0.5);
}

#nav {
  background-color: #f1c40f;
  border-radius: 0 0 12px 12px;
  max-height: 60px;
  height: 60px;
  overflow: hidden;
}
</style>

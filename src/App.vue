<template>
  <div id="app" class="container-fluid">
    <div id="nav" class="p-1 pl-3 mb-5">
      <div class="row">
        <div class="col-md-7">
          <router-link to="/">
            <img src="@/assets/logo.png" id="logo">
          </router-link>
        </div>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss" scoped>
#logo {
  width: 350px;
  filter: brightness(0.5);
}

#nav {
  background-color: #f1c40f;
  border-radius: 0 0 12px 12px;
  max-height: 60px; 
  overflow:hidden;
}
  </style>

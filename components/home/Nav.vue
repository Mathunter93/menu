<template>
  <nav class="d-flex align-items-center flex-row open-sans position-relative">
    <p class="a-logo">
      A
    </p>

    <p class="">
      BRAND NAME <br> <span> All Stores </span>
    </p>



    <div class="icon-set">
      <img src="~/static/bell.png" alt="">
      <img src="~/static/user2.png" alt="" >
      <button class="btn open-sans" @click="logout">
        logout
      </button>
    </div>

  </nav>
</template>

<script>
export default {
    name: "Navbar",
    methods: {
      logout() {
        localStorage.removeItem("menu_user");
        location.reload();
      }
    }
}
</script>

<style lang='scss'>
@import '~/assets/css/main.scss';
nav {
  background-color: $white_color;
  width: 100%;
  box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.15);
  height: 60px;
  z-index: 500;

  .a-logo {
    @include font-design(normal, 600, 17px, 30px, -0.408px);
    @include rad-pad-mar(50%, "", 14px 20px);
    width: 32px;
    height: 32px;
    text-align: center;
    background: $primary_color;
    color: $white_color;
  }

  p {
    &:nth-of-type(2) {
      @include font-design("", "", 11px, 12px, 0.066px);
      @include rad-pad-mar("", "", 14px 0);
      text-transform: uppercase;
      color: $grey_six;

      span {
        @include font-design(normal, 700, 14px, 22px, -0.154px);
        color: #141414;
      }
    }
  }

  .icon-set {
    position: absolute;
    right: 32px;
    top: 14px;
    
    img {
      width: 18px;
      height: 20px;
      margin-left: 19px;
    }

    button {
      @include rad-pad-mar(4px, 7px 12px, 0 10px);
      @include font-design("", 600, 14px, 14px, -0.154px);
      @include box-shadow(0px 1px 0px rgba(0, 0, 0, 0.08), inset 0px -1px 0px rgba(0, 0, 0, 0.1));
      background: $primary_color;
      color: $white_color;
      gap: 4px;     
      text-align: center;
      text-transform: capitalize;  
    }
  }

}

</style>
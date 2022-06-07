<template>
  <div class="login_carousel">
      <div class="row">
          <div class="col-4">
              <Shapes 
              :combination="'shape_holder'"
              />
          </div>
          <div class="col-4">
              <Shapes 
              
              :combination="'shape_holder_reverse'"/>
          </div>
          <div class="col-4">
              <Shapes 
              
              :combination="'shape_holder'"/>
          </div>
      </div>
  </div>
</template>

<script>
import Shapes from "./Shapes.vue"
export default {
    data() {
        return {

        }
    },
    components: {
        Shapes
    }
}
</script>

<style lang='scss'>
@import '~/assets/css/main.scss';
.login_carousel {
    @include position-absolute("", "", "", 10%);
    @include box-shadow(0px 0px 2px 2px rgba(0, 0, 0, 0.075));
    width: 80vw;
    height: 100vh;
    margin: 0 auto;
    background-color: orange;
    overflow: hidden;
    .col-4 {
        height: 100vh;
        @include box-shadow(0 0 2px 2px rgba(0, 0, 0, 0.068));
    }
}

</style>
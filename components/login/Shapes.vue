<template>
  <div class=""
  :class="combination"
  >
      <div class="shape" v-for="(shape, index) in shape_combo" :key="index">
          <div :class="shape"></div>
      </div>    
  </div>
</template>

<script>
export default {
    props: [
        'combination'
    ],
    data() {
        return {
            shapes: [
                "shape-circle", "triangle-top-right", "diamond-shape", "triangle-bottom-left", "half-circle-bottom"
            ],
            shape_combo: []
        }
    },
    methods: {
        shape_combination() {
            let arr = [...this.shapes, ...this.shapes]
            
            let num = arr.length
            
            for(let i= 0; i<num; i++){

                let checker = Math.floor(Math.random() * 10);
                // console.log(checker)
                this.shape_combo.push(arr[checker])

            }

        }
    },
    mounted() {
        this.shape_combination()
    }
}
</script>

<style lang='scss'>
@import '~/assets/css/main.scss';

$red : red;

.shape_holder {
    @include position-absolute("", "", 0, 0);
    width: 100%;
    height: 300vh;
    animation: MoveUpDown 45s linear infinite;
    background-color: $red;
}
.shape_holder_reverse {
    @extend .shape_holder;
    animation: MoveDownUp 45s linear infinite;
}

@keyframes MoveDownUp {
  50% {
    bottom: 0;
  }
  0%, 100% {
    bottom: 150vh;
  }
}

@keyframes MoveUpDown {
  0%, 100% {
    bottom: -150vh;
  }
  50% {
    bottom: 0;
  }
}
.shape {
    width: 100%;
    height: calc(80vw / 3);
    background-color: #FF7D26;
    overflow: hidden;
    &:nth-of-type(2n){
        background-color: $secondary_color;
    }
}
.full_size {
    width: 100%;
    height: 100%;
}
.shape-circle {
    @extend .full_size;
    background: $primary_color;
    border-radius: 50%;
}
.triangle-top-right {
    @extend .full_size;
	border-width: 0 calc(80vw / 3) calc(80vw / 3) 0;
	border-color: transparent $third_color transparent transparent;
	border-style: solid;
}
.triangle-bottom-left {
    @extend .full_size;
    border-width: calc(80vw / 3) 0 0 calc(80vw / 3);
	border-color: transparent transparent transparent $third_color;
	border-style: solid;
}
.diamond-shape {
    width: 70%;
    height: 70%;
    background-color: $primary_color;
    margin: 15%;
    /* border: 50px solid transparent; */
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);

}
.half-circle-bottom {
    height:60%;
    width: calc(50% * 2);
    border-bottom-left-radius: 50%;
    border-bottom-right-radius: 50%;
    background-color: $primary_color;
}
</style>
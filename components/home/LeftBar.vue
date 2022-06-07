<template>
  <div class="left-bar d-flex flex-column open-sans">
      <div v-for="(side, index) in side_pills" :key="index"
      class="left-pill d-flex align-items-center"
      >
      <b-img :src="side.image"></b-img>
         {{side.name}}
      </div>
  </div>
</template>

<script>
export default {
    name: "Leftbar",
    data() {
        return {
            side_pills: [
                {
                    name: "Analytics",
                    image: "Analytics.png"
                },
                {
                    name: "Offers",
                    image: "Iconoffer.png"
                },
                {
                    name: "Loyalty",
                    image: "user.png"
                },
                {
                    name: "Currencies",
                    image: "Vectorcrr.png"
                },
                {
                    name: "Dispatch",
                    image: "Analytics.png"
                },
                {
                    name: "Configurations",
                    image: "settings.png"
                }
            ]
        }
    }
}
</script>

<style lang='scss'>
@import '~/assets/css/main.scss';
.left-bar {
    @include position-absolute("", "", "", 0);
    width: 17%;
    height: calc(100vh - 62px);
    padding: 8px 0px;
    background: #F2F2F2;
    .left-pill {
        @include font-design("", 400, 14px, 22px, -0.154px);
        @include rad-pad-mar(4px, "", 0 auto 11px auto);
        width: calc(100% - 24px);
        height: 40px;
        color: #141414;

        img {
            margin-left: 13px;
            margin-right: 12px;
        }
        
        &:hover {
            background: rgba(255, 102, 0, 0.07);
            color: #FF6600;
        }
    }
}

</style>
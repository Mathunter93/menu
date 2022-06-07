<template>
    <div class="currency-nav">
          <div>
            <p class="float-left">
              Currencies
            </p>

            <button class="float-right d-flex align-items-center" @click="open_side">
              <img src="~/static/Iconplus.png" alt="">
               Add Currency
            </button>
          </div>

          <div class="clearfix w-100"></div>

          <div class="search-nav d-flex align-items-center">

            <img src="~/static/Iconmagnify.png" alt="" class="mx-2">

            <input type="text" name="" id="searchbar" placeholder="Search" @keyup="$emit('search_filter')" v-model="search_text">

          </div>
         

    </div>
</template>

<script>
export default {
    methods: {
        
    }
}
</script>

<style>

</style>
<template>
  <div class="display-window">

      <div class="currency-display"
      :class="[{ col_8 : side_area }, { col_12: !side_area }]"
      >

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

            <input type="text" name="" id="searchbar" placeholder="Search" @keyup="search_filter" v-model="search_text">

          </div>
         

        </div>

        <div class="currency-list">
          
          <div class="row text-left pl-1 table-head">
            <div class="col-7" >
              <p>
                Currency Name
              </p>
            </div>

            <div class="col-2">
              <p>
                Currency Code
              </p>
            </div>

            <div class="col-2">
              <p>
                Currency Symbol
              </p>
            </div>

            <div class="col-1 text-right">
              <p>
                
              </p>
            </div>
          </div>


          <div class="row text-left pl-1 curr-data d-flex align-items-centter" v-for="(currency, index) in control_currencies" :key="index">
            <div class="col-7 d-flex align-items-center" @click="open_edit(index)">
              <p>
                {{currency.name}}
              </p>
            </div>

            <div class="col-2 d-flex align-items-center" @click="open_edit(index)">
              <p>
                {{currency.code}}
              </p>
            </div>

            <div class="col-2 d-flex align-items-center" @click="open_edit(index)">
              <p>
                {{currency.symbol}}
              </p>
            </div>

            <div class="col-1 text-right d-flex align-items-center" @click="delete_one(currency)">
              <img src="~/static/Deletede.png" alt="" >
            </div>

          </div>


        </div>
         
      <div class="clear-both"></div>


      </div>

      <div class="currency-side-bar"  v-if="side_area"
      :class="[{ col_4 : side_area }]"
      >
        <div v-if="mode == 'add'">        
        <div class="side-action open-sans d-flex justify-content-between align-items-center" 
        :class="[{ green_bg: added_success }, { red_bg: added_fail }]"
        
        >
          <div > 
            <p>
             <span @click="close_side"> X </span> Add Currency
            </p>

          </div>
         

          <div class="buttons">

              <button @click="close_side">
                Cancel
              </button>
              
              <button @click="add_new">
                Add
              </button>

          </div>

        </div>


        <div class="form-fields d-flex flex-column open-sans">
          <div >
              <b-form  @submit.stop.prevent>
                <label for="curr-name">Currency Name</label>
                <b-form-input v-model="name" id="curr-name"></b-form-input>
                <b-form-invalid-feedback :state="validation">
                  Your user ID must be 5-12 characters long.
                </b-form-invalid-feedback>
                <b-form-valid-feedback :state="validation">
                  
                </b-form-valid-feedback>
              </b-form>

          </div>

          <div>
              <b-form  @submit.stop.prevent>
                <label for="curr-code">Currency Code</label>
                <b-form-input v-model="code" id="curr-code"
                @keyup="valid_code"
                ></b-form-input>
                <b-form-invalid-feedback :state="code_valid">
                  Code must me 3 letters long and unique
                </b-form-invalid-feedback>
                <b-form-valid-feedback :state="code_valid">
                  
                </b-form-valid-feedback>
              </b-form>

          </div>

          <div>
              <b-form @submit.stop.prevent>
                <label for="curr-symbol">Currency Symbol</label>
                <b-form-input v-model="symbol" id="curr-symbol"
                @keyup="symbol_validation"
                @keyup.enter="insert_enter"
                ></b-form-input>
                <b-form-invalid-feedback :state="symbol_valid">
                  Please enter a valid symbol
                </b-form-invalid-feedback>
                <b-form-valid-feedback :state="symbol_valid">
                 
                </b-form-valid-feedback>
              </b-form>

          </div>
        </div>
        </div>

        <div v-if="mode == 'edit'">        
        <div class="side-action open-sans d-flex justify-content-between align-items-center">
          <div > 
            <p>
             <span @click="close_side"> X </span>  Edit Currency
            </p>

          </div>
         

          <div class="buttons">

              <button @click="close_side">
                Cancel
              </button>
              
              <button @click="save_change">
                Save
              </button>

          </div>

        </div>


        <div class="form-fields d-flex flex-column open-sans">
          <div >
              <b-form  @submit.stop.prevent>
                <label for="curr-name">Currency Name</label>
                <b-form-input v-model="name" id="curr-name"  @keyup="valid_name"></b-form-input>
                <b-form-invalid-feedback :state="validation" >
                  Your user ID must be 5-12 characters long.
                </b-form-invalid-feedback>
                <b-form-valid-feedback :state="validation">
                  
                </b-form-valid-feedback>
              </b-form>

          </div>

          <div>
              <b-form  @submit.stop.prevent>
                <label for="curr-code">Currency Code</label>
                <b-form-input v-model="code" id="curr-code"
                @keyup="valid_code"
                ></b-form-input>
                <b-form-invalid-feedback :state="code_valid">
                  Code must me 3 letters long and unique
                </b-form-invalid-feedback>
                <b-form-valid-feedback :state="code_valid">
                  
                </b-form-valid-feedback>
              </b-form>

          </div>

          <div>
              <b-form @submit.stop.prevent>
                <label for="curr-symbol">Currency Symbol</label>
                <b-form-input v-model="symbol" id="curr-symbol"
                @keyup="symbol_validation"
                ></b-form-input>
                <b-form-invalid-feedback :state="symbol_valid">
                  Please enter a valid symbol
                </b-form-invalid-feedback>
                <b-form-valid-feedback :state="symbol_valid">
                 
                </b-form-valid-feedback>
              </b-form>
          </div>
        </div>
        </div>



        
      </div>
     

  </div>
</template>

<script >
export default {
  data() {
    
    return {
      side_area: false,
      fields: [
        {
          label: "name",
          valid: "name_valid",
          function: "name_checker"
        }
      ],
      mode: "add", //changes between add and edit depending on the side section
      search_text: "", 
      edit_id: null, //comparrison for editing
      id: null, //comparrison for editing
      name: "",
      code: "",
      symbol: "",
      validation: true, //name validation
      code_valid: null, //code validation
      symbol_valid: null,
      test_message: "",
      added_success: false, //used to trigger bg based on add/edit function
      added_fail: false,
      edit_success: false,
      edit_fail: false,
      existing_codes: [],
      edit_codes: [],
      control_currencies: [],
      currencies: []
    }
  },
  methods: {
    add_new() {

      //Validation process
      if(this.validation && this.symbol_valid && this.code_valid) {

        let id
        
        //logic for unique ID assignment
        if(this.currencies.length == 0){
          id = 0
        }
        else {
          //get all IDs if this.currencies is not empty
          let current_ids = Array.from(this.currencies, currency => currency.id)
          id = 0

          //set ID to the next biggest (this could have been done with uniquid or something in that sort)
          while(current_ids.includes(id)){
            id += 1
          }
        }

        //prepare object
        let new_curr = {
          id: id,
          name: this.name,
          code: this.code.toUpperCase(),
          symbol: this.symbol
        }
        //send
        this.currencies.push(new_curr)
        //make both lists equal
        this.control_currencies = this.currencies

        this.save_local() //saves to localstora
        this.clear_data() //clears this. name, code, symbol

        //trigger green bg
        this.added_success = true
        setTimeout(() => {
          //close green bg
          this.added_success = false
        }, 200)
      }else {
        //trigger red bg
        this.added_fail = true
        setTimeout(() => {
          //close red bg
          this.added_fail = false
        }, 200)
      }
      
    },

    insert_enter(e) {
      //focus on first (name) field upon successfull entry completion
      if(e.key === "Enter"){
        this.add_new()
        document.getElementById("curr-name").focus();
        document.getElementById("curr-name").select();
      }
    },

    valid_name() {

      let code = this.name.toUpperCase()

      let names = Array.from(this.currencies, currency => currency.name.toUpperCase())

      if(names.includes(code)){
        this.validation = false
      }else {
        this.validation = true
      }
      
    },

    valid_code() {
      
      
      let code = this.code.toUpperCase()
      let existing_codes = []
      let edit_codes     = []
      // console.log(this.currencies)
      if(this.currencies.length != 0){
        existing_codes = Array.from(this.currencies, currency => currency.code.toUpperCase())

        edit_codes = Array.from(this.currencies, currency => 
            currency.code.toUpperCase() 
        )
      }
    
      let regex = this.code_letters(code)

      if(((existing_codes.includes(code) && this.mode == "add") || this.mode == "edit") || code.length != 3 || !regex) {
        
        if(this.mode == "edit" && (this.currencies[this.id].code == code || !existing_codes.includes(code))){
          this.code_valid = true
        }else {

           this.code_valid = false
        }
       
      }else {

        this.code_valid = true
      }
      

    
    },
    code_letters(str) {
      return /^[A-Za-z\s]*$/.test(str);
    } ,

    symbol_validation() {

      let symbol = this.symbol

      if(symbol.length == 0 || symbol.length > 4){
        this.symbol_valid = false
      }else {
        this.symbol_valid = true
      }

    },

    delete_one(x) {
      if(x.name == this.name){
        this.clear_data() //clears this. name, code, symbol
        this.id         = ""
        this.edit_id    = ""
      }
      let index = this.currencies.indexOf(x);
      let control_index = this.control_currencies.indexOf(x)      
      this.currencies.splice(x, 1)
      // this.control_currencies.splice(x, 1)
      this.side_area = false
      
      this.save_local()
    },

    open_side() {
      this.mode       = "add"
      this.clear_data() //clears this. name, code, symbol
      this.side_area  = true
    },
    close_side() {
      this.side_area = false
    },
    save_change() {
      
      if(this.validation && this.symbol_valid && this.code_valid) {

        this.currencies[this.id].name = this.name 
        this.currencies[this.id].code = this.code.toUpperCase(),
        this.currencies[this.id].symbol = this.symbol

        this.save_local()        
        this.clear_data() //clears this. name, code, symbol

        this.side_area = false
      }else {
        alert("try again")
        
      }

    },

    open_edit(x){

      this.validation     = true 
      this.symbol_valid   = true
      this.code_valid     = true
      this.mode       = "edit"
      this.side_area  = true
      this.id         = x
      this.edit_id    = this.currencies[x].id
      this.name       = this.currencies[x].name
      this.code       = this.currencies[x].code
      this.symbol     = this.currencies[x].symbol
    },

    search_filter() {
      this.control_currencies = this.currencies.filter(cur => {
            return cur.name.toLowerCase().includes(this.search_text.toLowerCase()) || cur.code.toLowerCase().includes(this.search_text.toLowerCase()) || cur.symbol.toLowerCase().includes(this.search_text.toLowerCase())
      })

    },

    save_local() {
      localStorage.setItem("currencies_menu", JSON.stringify(this.currencies));
    },
    clear_data() {
      this.name   = ""
      this.code   = ""
      this.symbol = ""
    }
  },
  mounted() {
    let curruencies = JSON.parse(localStorage.getItem("currencies_menu"));
    if(curruencies === null) {
      this.currencies = []
      this.control_currencies = []
    }else {
      this.currencies = curruencies
      this.control_currencies = curruencies
    }
  }
}
</script>

<style lang='scss'>
@import '~/assets/css/main.scss';
button {
  border: 1px solid rgba(255, 255, 255, 0);
}
.display-window {
    height: calc(100vh - 75x);
    width: 83%;
    left: 17%;
    float: right; 

    .currency-nav {
      @include rad-pad-mar("", "", 32px 32px 24px 32px);
      width: calc(100% - 40px);
      height: 92px;    

      div {
        p {
          @include font-design("", 700, 28px, 32px, 0.364px);
          color: #141414;
        }
        button {
          @include rad-pad-mar(4px, 7px 12px, "");
          @include font-design("", 600, 14px, 14px, -0.154px);
          @include box-shadow(0px 1px 0px rgba(0, 0, 0, 0.08), inset 0px -1px 0px rgba(0, 0, 0, 0.1));
          background: $primary_color;
          color: $white_color;
          gap: 4px;
          width: 137px;
          height: 34px;        
          text-align: center;
        }
      }
      .search-nav {
        @include rad-pad-mar(4px, 6px 4px, 4px 0 0 0);
        height: 34px;
        width: 30%;
        border: 1px solid #CCCCCC;


        input {
          border: 1px solid $white_color;
          width: 100%;
          &:focus {
            border: 1px solid red;
          }
        }
      }
        
    }

    .currency-list {
      @include font-design("", 600, 11px, 12px, 0.066px);
      margin: 32px 32px 24px 32px;
      width: calc(100% - 40px);
      height: 92px;
      text-transform: uppercase;
      color: $grey_six;

      .row {
        border-bottom:1px solid rgba(0, 0, 0, 0.07);
      }
      .curr-data {
        p {
          @include font-design(normal, 600, 14px, "", -0.154px);
          padding: 10px 0 0 0;
          color: #141414;
        }
        &:hover {
          background: rgba(0, 0, 0, 0.03);
          cursor: pointer;
        }
      }
    }
}
.currency-display {
  display:inline-block;
}

.currency-side-bar {
  height: calc(100vh - 70px);
  border-left: 1px solid rgba(0, 0, 0, 0.07);
  float: right;

  .side-action {
    @include flex-center();
    @include rad-pad-mar("", 12px 24px 12px 16px, "");
    @include box-shadow(0px 1px 1px rgba(0, 0, 0, 0.15));
    height: 58px;
    width: 100%;
    flex-direction: row;
    div {
      p {
        @include font-design(normal, 700, 17px, 22px, -0.408px);
        height: 22px;
        padding-top: 7px;
        color: #141414;
        span {
          width: 13px;
          height: 13px;
          color: $grey_six;
          margin-right: 18px;
        }
      }
    }
    button {
      @include flex-center();
      @include rad-pad-mar(4px, 7px 12px, 0 0 0 8px);
      @include box-shadow(0px 1px 0px rgba(0, 0, 0, 0.06));
      gap: 4px;
      width: 71px;
      height: 34px;
      background: $white_color;
      border: 1px solid #CCCCCC;
      flex-direction: row;
      float: left;
      &:nth-of-type(2) {
        background: #FF6600;
        color: $white_color;
      }
    }
  }
}
.clear-both {
  clear: both;
}

.form-fields{
  padding: 16px 36px;
}
.green_bg {
  background-image: linear-gradient(to right, rgba(0, 128, 0, 0.698),  green) !important;
  @include transition(background-image, 200ms, linear);
}
.red_bg {
 background-image: linear-gradient(to right, rgba(255, 0, 0, 0.701),  red) !important;
 @include transition(background-image, 200ms, linear);
}
.col_4 {
  width: calc(100% / 12 * 4);
}
.col_8 {
  width: calc(100% / 12 * 8);
}
.col_12 {
  width: 97%;
}
</style>
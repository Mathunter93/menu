<template>
<div class="login-holder">
    <div class="login-page d-flex justify-content-center align-items-center">
        <LoginHolder />
        <div class="login-form open-sans">

            <div class="logo-cover d-flex justify-content-center align-items-center">
                <img src="~/static/Mlogo.png" alt="loginlogo">
            </div>

            <div class="text-left open-sans">
                <p>Sign in <br>
                <span>Please enter your email and password</span></p>
            </div>


            <div class="login-input-cover w-100 open-sans" @submit="sign_in">
                <input type="email" class="login-input mb-2" placeholder="Your email address" v-model="username">
                <input type="password" class="login-input"  placeholder="Password" v-model="password">
            </div>

            <button class="sign-in-button text-center" @click="sign_in">
                Sign in
            </button>

        </div>
        
        

  </div>
</div> 
</template>

<script lang='ts'>

export default {
    name: "Login",

    head: {
      title: "Menu Technology | Login",
    },
    data() {
        let username: String = ""
        let password: String = ""

        return {
           username,
           password
        }
    },
    methods: {
        sign_in(): Boolean {
            if(this.username !== "" && this.password !== "" ){
            let user = {
                username: "matei",
                logged: true
            }

            localStorage.setItem("menu_user", JSON.stringify(user));
            location.reload();

            return
            }
        }
    }
}
</script>

<style lang='scss'>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500&display=swap');
@import '~/assets/css/main.scss';

.open-sans {
    font-family: $main-font;
}

.login-holder {
    background-color: rgba(255, 125, 38, 0.923);
}
.login-page {
    width: 100vw;
    height: 100vh;
    background-color: rgba(180, 117, 0, 0.492);
    background-size: auto 100%;
    overflow: hidden;

    .login-form {
        @include rad-pad-mar(8px, 40px, "");
        width: 376px;
        height: 384px;
        background-color: $white_color;
        box-shadow: 0px 0px 0px 1px rgba(0, 0, 0, 0.05), 0px 5px 20px rgba(0, 0, 0, 0.1);
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 24px;
        z-index: 1500;

        .logo-cover {
            @include rad-pad-mar(4px, "", "");
            width: 40px;
            height: 40px;
            background: $primary_color;

            img {
                width: 16.95px;
                height: 23.52px;
            }
        }

        p {
            @include font-design(normal, 700, 22px, 28px, 0.352px);
            span {
                @include font-design(normal, 400, 14px, 22px, -0.154px);
            }
        }
        .login-input {
            @include rad-pad-mar(4px, 6px 9px 6px 12px, "");
            height: 34px;
            width: 100%;
            border: 1px solid #CCCCCC;
        }
        .sign-in-button {
            @include flex-center();
            @include font-design(normal, 600, 14px, 20px, -0.154px);
            @include rad-pad-mar(4px, 7px 12px, "");
            width: 100%;
            height: 34px;
            flex-direction: row;
            background: $primary_color;
            box-shadow: 0px 1px 0px rgba(0, 0, 0, 0.08), inset 0px -1px 0px rgba(0, 0, 0, 0.1) !important;
            color: $white_color;
            text-align: center;

        }
    }
}

input:focus {
    box-shadow: 0px 0px 0px 1.5px rgba(255, 102, 0, 0.6) !important; 
    border: 1.5px rgba(255, 102, 0, 0.6) !important;
}


</style>
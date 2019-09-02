<template>
<div class="col-sm-8 container d-flex align-items-center justify-content-center">
    <div class="login-card">
        <h2 class="title"> Desafio BossaBox - Login</h2>
        <form @submit="login">
            <div class='row'>
                <div class='col'>
                    <label> E-mail </label>
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input type="text" v-model="email" class="input-text" required/>
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <label> Password </label>
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input type="password" v-model="senha" class="input-text" required/> 
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input type="button" @click="signUpPage" class="signup-button" value="Sign Up"/>
                    <input type="submit" class="submit-button" value="Login"/>
                </div>
            </div>
        </form>
    </div>
</div>
</template>

<script>
import router from "../router";
import axios from "axios";

export default {
  name: "sign-in-page",
  data() {
    return {
        email: "",
        senha: ""
    };
  },
  methods: {
    login() {
        axios.post("http://localhost:3000/signin", { 
            email: this.email, 
            senha: this.senha
        })
        .then((response) => {
            localStorage.setItem("access-token", response.data.result);
            router.push({ name: "home" }); 
        })
        .catch((response) => {
            alert("Email or password incorrect.")
        });   
    },
    signUpPage(){
        router.push({ name: "signup" }) ;
    }
  }
};
</script>

<style scoped>

.container {
    height: 100vh;
}

.input-text {
    background: #f5f4f6 0% 0% no-repeat padding-box;
    border: 1px solid #ebeaed;
    border-radius: 5px;
    opacity: 1;
}

.input-text:active {
    background: #ebeaed 0% 0% no-repeat padding-box;
    border: 1px solid #dedce1;
}

.submit-button {
    background: #365df0 0% 0% no-repeat padding-box;
    border: none;
    border-radius: 5px;
    opacity: 1;
    text-align: center;
    font: Semibold 18px/24px Source Sans Pro;
    letter-spacing: 0.36px;
    color: #ffffff;
    margin: 15px;
}

.submit-button:hover {
    background: #2f55cc 0% 0% no-repeat padding-box;
}

.submit-button:active {
    background: #244aa8 0% 0% no-repeat padding-box;
}

.signup-button {
    background: #e1e7fd 0% 0% no-repeat padding-box;
    border: none;
    border-radius: 5px;
    opacity: 1;
    text-align: center;
    font: Semibold 18px/24px Source Sans Pro;
    letter-spacing: 0.36px;
    color: #365df0;
    margin: 15px;
}

.signup-button:hover {
    background: #cad6fc 0% 0% no-repeat padding-box;
}

.back-button:active {
    background: #b9c6fa 0% 0% no-repeat padding-box;
}

.login-card {
    background: #ffffff 0% 0% no-repeat padding-box;
    box-shadow: 0px 5px 7px #0000000d;
    border: 1px solid #ebeaed;
    border-radius: 5px;
    opacity: 1;
    overflow: hidden;
    padding: 15px;
}

.title {
    font: Semibold 36px/40px Source Sans Pro;
}

</style>

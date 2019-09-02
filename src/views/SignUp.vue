<template>
<div class="col-sm-6 container d-flex align-items-center justify-content-center">
    <div class="login-card">
        <h2 class="title"> Desafio BossaBox - SignUp</h2>
        <form @submit="createUser">
            <div class='row'>
                <div class='col'>
                    <label> Name </label>
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input 
                        type="text" 
                        v-model="nome" 
                        class="input-text" 
                        required
                    />
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                <label> E-mail </label>
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input 
                        type="text" 
                        v-model="email" 
                        class="input-text" 
                        required
                    />  
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <label> Password </label>
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input 
                        type="password" 
                        v-model="senha" 
                        class="input-text" 
                        required
                    />      
                </div>
            </div>
            <div class='row'>
                <div class='col'>
                    <input 
                        type="button" 
                        @click="backClicked" 
                        class="back-button" 
                        value="Back"
                    />
                    <input 
                        type="submit" 
                        class="submit-button" 
                        value="Create"
                    />  
                </div>
            </div>
        </form>
    </div>
</div>
</template>

<script>
import axios from 'axios';
import router from '../router';

export default {
  name: "sign-up-page",
  data() {
    return {
        nome: '',
        email: '',
        senha: ''
    }
  },
  methods: {
    createUser() {
        axios.post('http://localhost:3000/signup', { nome: this.nome, 
            email: this.email, 
            senha: this.senha
        })
        .then((response) => {
            alert("Created with success.");
            router.push({ name: "signin" }); 
        })
        .catch((response) => {
            alert("User already created.");
        });   
    },
    backClicked(){
        router.push({ name: 'signin' }); 
    }
  }
};
</script>

<style scoped>
.title {
    text-align: left;
    font: Semibold 36px/40px Source Sans Pro;
    letter-spacing: 0.72px;
    color: #170C3A;
    opacity: 1;
}

.container {
    height: 100vh;
}

.input-text {
    background: #F5F4F6 0% 0% no-repeat padding-box;
    border: 1px solid #EBEAED;
    border-radius: 5px;
    opacity: 1;
}

.input-text:active {
    background: #EBEAED 0% 0% no-repeat padding-box;
    border: 1px solid #DEDCE1;
}

.submit-button {
    background: #365DF0 0% 0% no-repeat padding-box;
    border: none;
    border-radius: 5px;
    opacity: 1;
    text-align: center;
    font: Semibold 18px/24px Source Sans Pro;
    letter-spacing: 0.36px;
    color: #FFFFFF;
    margin: 15px;
}

.submit-button:hover {
    background: #2F55CC 0% 0% no-repeat padding-box;
}

.submit-button:active {
    background: #244AA8 0% 0% no-repeat padding-box;
}

.back-button {
    background: #E1E7FD 0% 0% no-repeat padding-box;
    border: none;
    border-radius: 5px;
    opacity: 1;
    text-align: center;
    font: Semibold 18px/24px Source Sans Pro;
    letter-spacing: 0.36px;
    color: #365DF0;
    margin: 15px;
}

.back-button:hover {
    background: #CAD6FC 0% 0% no-repeat padding-box;
}

.back-button:active {
    background: #B9C6FA 0% 0% no-repeat padding-box;
}

.login-card {
    background: #FFFFFF 0% 0% no-repeat padding-box;
    box-shadow: 0px 5px 7px #0000000D;
    border: 1px solid #EBEAED;
    border-radius: 5px;
    opacity: 1;
    overflow: hidden;
    padding: 15px;
}

.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

</style>

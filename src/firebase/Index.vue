<template>
    <div>
        <h1>Enter number</h1>
          <input type="text" v-model="number" placeholder="+998*********" required>
          <div id="recaptcha-container"></div>
          <button type="submit" @click="phoneAuth();">SendCode</button>

          <br>
          <h1>Verification code</h1>
          <input type="text" id="verificationCode" placeholder="Enter verification code" required>
          <button type="submit" onclick="codeverify();">Verify code</button>
    </div>
</template>

<script>
export default {
  data(){
    return{
      number:'',
      code:'',
      auth: null
    }
  },
  mounted () {    
    // console.log(firebase);
    this.auth= new firebase.auth.RecaptchaVerifier('recaptcha-container');
    this.auth.render();
  },
  methods:{
    phoneAuth(){      
      firebase.auth().signInWithPhoneNumber(this.number, this.auth)
        .then(function(confirmationResult){
            const codeResult = confirmationResult;
            console.log('confirmationResult',codeResult)
        }).catch(function(error){
            console.log('error',error)
        })
    }
  }
}
</script>

<style>

</style>
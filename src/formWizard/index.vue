<template>
    <div>
        <form>
          <section v-show="step == 1">
            <h1>step1</h1>
              <el-input style="width:20%"  placeholder="Enter Your Username" @input="removeErrorMsg();" v-model="form.name"></el-input>
          </section>
          <section v-show="step == 2">
            <h1>step2</h1>
             <div>
                <el-input id="ok" style="width:20%"  ref="number" v-model="form.phone" type="text" placeholder="Enter Phone" @input="removeErrorMsg();"></el-input>
              <el-input style="width:20%" v-model="form.email" type="text" placeholder="Enter Email" @input="removeErrorMsg();"></el-input>
             </div>
          </section>
          <section v-show="step == 3">
            <h1>step3</h1>
            <textarea v-model="form.message" placeholder="type your message" @input="removeErrorMsg();"></textarea>
          </section>
            <span style="color:red">{{error}}</span> <br>
            <el-button type="success"  v-if="step != 1" @click.prevent="prevStep();">prevStep</el-button>
            <el-button v-if="step != totalStep" @click="nextStep();">nextStep</el-button>
            <el-button v-if="step == 3" @click.prevent="nextEnquiry();">nextEnquiry</el-button>
        </form>
    </div>
</template>

<script>
    import IMask from 'imask';
    export default {
        data(){
          return{
            step:1,
            totalStep:3,
            error:'',
            form:{
              name:null,
              email:null,
              phone:null,
              message:null
            }
          }
        },

        mounted () {
          
        },

        methods:{
          numberMask(){
            console.log('sdd')
              const element = this.$refs['number'];
                const maskOptions = {
                  mask: '+{998}(00)000-00-00',
                };
              IMask(element, maskOptions);
            },
          removeErrorMsg(){
            this.error = ''
          },
          errorMesage(input){
            this.error = 'Please fill out your ' + input
          },
          nextStep(){
            if(this.step == 1){
              if(!this.form.name){
                this.errorMesage('name')
                // this.removeErrorMsg();
                return false;
              }
            }
             if(this.step == 2){
               console.log("SSSSSSSSSSSSS")
               setTimeout(() => {
                console.log("AAAAA")
                IMask(
                document.getElementById('ok'), {
                  mask: '+{7}(000)000-00-00'
                });
              }, 2000)
              if(!this.form.email){
                this.errorMesage('email')
                // this.removeErrorMsg();
                return false;
              }
              if(!this.form.phone){
                  this.errorMesage('phone')
                // this.removeErrorMsg();
                return false;
              }
              
            }
            // this.error = '';

            this.step++;
            this.removeErrorMsg();
          },
          prevStep(){
            this.step--;
          },
          nextEnquiry(){
              if(!this.form.message){
                this.error = 'Please fill out are!';
                return false;
              }
              this.error = '';
          alert('this has been sent');
            
            for(let key in this.form){
              this.form[key] = ''
            }
            this.removeErrorMsg();
            this.step = 1
          }
        }
    }
</script>

<style>
  textarea{
    border: none;
  }
</style>
<template>
  <div id="app">
  <h1>Vue Events</h1>
  <h2>Events in Action</h2>
  <button v-on:click="increement()">
    Add
  </button>
  <button v-on:click="decreement()">
    Subtract
  </button>
  <p>Result:{{counter}}</p>
  <!-- We are outputting the name over here in the input element ober here as the name is dyanmic so we are using the v- bind over here-->
  <!-- Over here we will now use v-model="Name" which will combine v-on:input and v-bind:value  and v-bind will handle the Name which is dynamically changing continuously-->
  <!-- <input type="text" 
  v-bind:value="Name"
  v-on:input="setName(event)" 
  v-on:keyup.enter="setConfirm()"/> -->
  <input type="text" v-model="FirstName"/>
  <input type="text" v-model="LastName"/>
  <button v-on:click="resetValue()">Reset Input</button>
  <p >Your Name:{{FirstName+ ' '+LastName}}</p>
  <form v-on:submit.prevent="submitForm()">
  <input type="text"/>
  <button>Sign Up!</button>
  </form>
  </div>
  <section id="styling">
  <div class="demo"  
  :class="boxAClasses" 
   @click="boxSelected('A')"></div>
  <div class="demo"  @click="boxSelected('B')"></div>
  <div class="demo"  @click="boxSelected('C')"></div>
  </section>
  </template>
  <script>
  export default({
    data() {
      return {
        counter: 0,
        FirstName:'',
        LastName:'',
        confirmedName:'',
        boxASelected:false,
        boxBSelected:false,
        boxCSelected:false
      }
    },
    watch:{
      FirstName(value){
        if(value===""){
          return "";
        }else{
          return value+' '+this.LastName;
        }
      },
      LastName(value){
        if(value===""){
          return "";

        }else{
          return this.FirstName+' '+value;
        }
      }
    },
    computed:{
      boxAClasses(){
        return {active:this.boxASelected};
      }
    },
    methods:{
      boxSelected(box){
        if(box==='A'){
          this.boxASelected=!this.boxASelected;
        }else if(box==='B'){
          this.boxBSelected=true;
        }else if(box==='C'){
          this.boxCSelected=true;
        }

      },
      resetValue(){
        this.FirstName='';
        this.LastName='';
      },
      submitForm(){
        alert('Submitted');
      },
      setConfirm(){
        this.confirmedName=this.Name;
      },
      setName(event){
        this.Name=event.target.value;
      },
      increement(){
          this.counter=this.counter+1;
      },
      decreement(){
          this.counter=this.counter-1;
      }
    }
  })
  </script>
  <style >
  #styling {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
}
.demo {
  width: calc(100% - 32px);
  height: 100px;
  margin: 16px;
  border: 2px dashed #ccc;
}
  h3 {
  margin: 40px 0 0;
}
button {
  font-weight: bold;
}
.active{
border-color: red;
background-color: salmon;
}
</style>
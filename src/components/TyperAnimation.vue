<template>
 <v-container>
   <v-layout column>
     <v-flex row>
       <span v-for="word in arr" class="words" style="width: fit-content"  v-if="word.visible">
       <template v-if="word.word === ' '">
         &nbsp
       </template>
       <template v-else>
         {{word.word}}
       </template>
         </span>
       <span class="pipe" v-bind:style="pipe? 'visibility:visible' : 'visibility:hidden'">   |</span>
     </v-flex>
     <v-flex style="margin-top: 40px">
       <v-btn @click="destroyText(`< Soy el typer />`)" >Agree</v-btn>
     </v-flex>
     <v-flex>
       <v-btn @click="cambio()">Cambio</v-btn>
     </v-flex>
   </v-layout>
 </v-container>

</template>

<script>
  export default{
    name:'TyperAnimation',
    props:['text'],
    data:function(){
      return{
        textToReady:'asdas',
        arr:[],
        pipe:true,
        pipeBlink:false,
        pos:0
      }
    }
    ,
    methods:{
      destroyText:function(textIn){
        let wordsArr = textIn.split(/(\s)/)
        let finalArr = []
        wordsArr.map((word) =>{
          if(word === ' '){
            finalArr.push(' ')
          }else{
            finalArr =  finalArr.concat(word.split(''))
          }
        })
        console.log("soy el array ",finalArr)
        this.arr = finalArr.map((word) => ({word:word, visible:false}))
      },
      cambio:function(){
        setInterval(() =>{
          if(this.pos !== this.arr.length){
            this.arr[this.pos].visible = true
            this.pos = this.pos + 1
          }else{
            this.blink(true)
          }
        },300)
      },
      blink:function(opt){
        if(opt){
          let interval = setInterval(()=>{
            this.pipe = !this.pipe
            !this.pipeBlink? clearInterval(interval):null
          },1000)
        }else{

        }
      }
    },
  }
</script>

<style>
.words{
  font-size: large;
}
.pipe{
  font-size: large;
}
</style>
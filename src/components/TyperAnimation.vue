<template>
 <v-container>
   <v-layout column align-center>
     <v-flex row :class="{'selectedText':selected}" >
       <span v-for="word in arr" class="words" v-if="word.visible">
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
       <v-btn @click="start()">Cambio</v-btn>
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
        selected:false,
        textToReady:'asdas',
        arr:[],
        pipe:true,
        pipeBlink:false,
        timesBlinks:5*2, //5 de fuera, *2 porque se cuenta el de oculto igual.
        timesSelected:3*2, //igual
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
        this.arr = finalArr.map((word) => ({word:word, visible:false}))
      },
      cambio:function(){
        var blinks = 0
        var writeAction = setInterval(() =>{
          if(this.pos !== this.arr.length){
            this.arr[this.pos].visible = true
            this.pos = this.pos + 1
          }else{
            blinks++
            this.selected = blinks > this.timesBlinks
            this.pipe = !this.pipe
            if(blinks > this.timesSelected + this.timesBlinks){
              clearInterval(writeAction)
              //Iniciar denuevo.
            }
          }
        },300)
      },
      start:function(){
        this.destroyText(` Hola soy el typer `)
        this.cambio()
      }
    },
  }
</script>

<style>
.words{
  font-size: 35px;
}
.pipe{
  font-size: 35px;
}
.halfSelected{
  width: 50%;
}
.selectedText{
  background-color: #707070;
  color: azure;
}
</style>
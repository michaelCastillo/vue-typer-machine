<template>
 <v-container>
   <v-layout column align-center>
     <v-flex row :class="{'selectedText':selected}" >
       <span v-for="word in actualText" class="words" v-if="word.visible">
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
        actualText:[],
        arr:[],
        pipe:true,
        pipeBlink:false,
        timesBlinks:4*2, //5 de fuera, *2 porque se cuenta el de oculto igual.
        timesSelected:2*2, //igual
        writeSpeed:100,
        textIndex:0,
      }
    }
    ,
    methods:{
      destroyText:function(texts){
        this.arr = texts.map((a_text)=>{
          let wordsArr = a_text.split(/(\s)/)
          let finalArr = []
          wordsArr.map((word) =>{
            if(word === ' '){
              finalArr.push(' ')
            }else{
              finalArr =  finalArr.concat(word.split(''))
            }

          })
          return finalArr.map((word) => ({word:word, visible:false}))
        })

      },
      cambio:function(){
        var blinks = 0
        var pos = 0
        var writeAction = setInterval(() =>{
          if(pos !== this.actualText.length){
            this.actualText[pos].visible = true
            pos = pos + 1
          }else{
            blinks++
            this.selected = blinks > this.timesBlinks
            this.pipe = !this.pipe
            if(blinks > this.timesSelected + this.timesBlinks){
              clearInterval(writeAction)
            }
          }
        },this.writeSpeed)
      },
      start:function(){
        this.destroyText(['typer','machine'])
        this.actualText = this.arr[this.textIndex]
        console.log("actual ",this.actualText)
        var waitTime = this.writeSpeed*(this.actualText.length+this.timesSelected + this.timesBlinks)
        this.cambio()
        setTimeout(()=>{
          this.clearTyper()
          this.textIndex = this.textIndex === (this.arr.length - 1 )? 0 : this.textIndex + 1
          this.start()
        },waitTime + 200)

      },
      clearTyper(){
        this.actualText = []
        this.selected = false
        this.pipe = true
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
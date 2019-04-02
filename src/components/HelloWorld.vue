<template>
  <v-app>
    <v-container>
      <v-layout column>
        <v-flex style="margin-top: 100px">
          <TyperAnimation/>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>


</template>

<script>
  import TyperAnimation from '../components/TyperAnimation';
export default {
  name: 'HelloWorld',
  components:{
    TyperAnimation
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

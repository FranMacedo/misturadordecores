<template>
  <v-container>
     <v-col
        class="d-flex justify-center"
      >
      <div class="d-flex justify-center align-center" 
      :style="{ 'background-color': color , 'height': '75vh', 'width': '100vh'}"
      >
        {{color}}

      </div>
      
      </v-col>
      <v-col
        class="d-flex justify-center"
      >
      <div>
      </div>
      </v-col>

  </v-container>
</template>

<script>

  export default {
     props: {
      color: String,
    },
    // data(){
    //    return{
    //      myStyle:{
    //         backgroundColor: this.color,
    //         height: "200px",
    //         width: "600px",
    //         }
    //        }
    //      }
  }
</script>

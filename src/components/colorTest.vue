<template>
  <v-container>
     <v-col
        class="d-flex justify-center"
      >
      <div >
        {{color}}
      </div>
      </v-col>
  </v-container>
</template>

<script>
  export default {
     props: {
      color: String,
    },
   
  }
</script>

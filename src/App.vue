<template>
  <v-app>
 <v-container>
   <div class="d-flex flex-wrap justify-center align-baseline">
   <div class="text-h2">Misturacor</div>
   <div class="text-h5">&#8226; Misturador de Cores</div>
   </div>
    <v-row>   
      <v-col cols="12" md="6"> 
        <v-row>
          <v-col cols="12" sm="6" >
            <div class="d-flex justify-center">Cor da Carlota</div>
            <v-color-picker v-model="color1m"
            dot-size="25"
            swatches-max-height="200"
            ></v-color-picker>
          </v-col>
          <v-col cols="12" sm="6" >
            <div class="d-flex justify-center">Cor do Francisco</div>
            <v-color-picker v-model="color2m"
            dot-size="25"
            swatches-max-height="200"
            ></v-color-picker>

          </v-col>
        </v-row>
          <v-btn-toggle
          v-model="toggle_exclusive"
          mandatory
          class="d-flex flex-wrap"
          >
            <v-btn
                v-for="t in types"
                :key="t"
                class="my-1 mx-1"
                @click="changeType(t)"
                small
                elevation="2"
                

              >
                {{ t }}
              </v-btn>
          </v-btn-toggle>
      </v-col> 
      <v-col 
        cols="12"
        md="6"
      > 
      <ColorArea :color="mixedColor" />
      </v-col> 
    </v-row>
  </v-container>
  </v-app>
</template>
<script>
  import ColorArea from './components/ColorArea'
  // import  from 'color-blend'
import * as colorBlend from "color-blend";

  // import colorTest from './components/colorTest'

  export default {
    components:{
      ColorArea,
      // colorTest
    },
   

    data: () => ({
      types: ["screen", "normal", "multiply", "overlay", "darken", "lighten", "colorDodge", "colorBurn", "hardLight", "softLight", "difference", "exclusion", "hue", "saturation", "color", "luminosity"],
      type: 'screen',
      color1: { r: 228, g: 216, b: 228, a: 1 },
      color2:{ r: 175, g: 67, b: 67, a: 1 },
        toggle_exclusive: undefined,

      mixedColor: "rgb(255, 0, 255)" 
    }),

    computed: {
      color1m: {
        get () {
          return this.color1
        },
        set (v) {
          this.color1 = v
          this.setMixedColor()

        },
      },
        color2m: {
        get () {
          return this.color2
        },
        set (v) {
          this.color2 = v
          this.setMixedColor()
        },
      },
   
    },
    mounted() {
          this.setMixedColor()
    },
    methods: {
      changeType(t){
      this.type= t
      this.setMixedColor()

      },

      useBlendType(){
        switch (this.type) {
            case 'screen':
              return colorBlend.screen(this.color1, this.color2)
            case 'normal':
              return colorBlend.normal(this.color1, this.color2)
            case 'multiply':
              return colorBlend.multiply(this.color1, this.color2)
            case 'overlay':
              return colorBlend.overlay(this.color1, this.color2)
            case 'darken':
              return colorBlend.darken(this.color1, this.color2)
            case 'lighten':
              return colorBlend.lighten(this.color1, this.color2)
            case 'colorDodge':
              return colorBlend.colorDodge(this.color1, this.color2)
            case 'colorBurn':
              return colorBlend.colorBurn(this.color1, this.color2)
            case 'hardLight':
              return colorBlend.hardLight(this.color1, this.color2)
            case 'softLight':
              return colorBlend.softLight(this.color1, this.color2)
            case 'difference':
              return colorBlend.difference(this.color1, this.color2)
            case 'exclusion':
              return colorBlend.exclusion(this.color1, this.color2)
            case 'hue':
              return colorBlend.hue(this.color1, this.color2)
            case 'saturation':
              return colorBlend.saturation(this.color1, this.color2)
            case 'color':
              return colorBlend.color(this.color1, this.color2)
            case 'luminosity':
              return colorBlend.luminosity(this.color1, this.color2)
            default:
              return colorBlend.screen(this.color1, this.color2)
          }
      },
   
      setMixedColor(){
        const mixedColor_ = this.useBlendType(this.color2, this.color1)
        this.mixedColor = this.formatObjectRGBA(mixedColor_)

        // console.log('1: ', this.formatObjectRGBA(this.color1))
        // console.log('2: ', this.formatObjectRGBA(this.color2))
        // console.log('mix: ', this.mixedColor)

      },
      formatObjectRGBA(color){
          return `rgba(${color['r']}, ${color['g']}, ${color['b']}, ${color['a']})`
      },
       formatArrayRGBA(color){
          return "rgba("+color.join(',')+")"
      }
    }
  }
</script>
<style>

body {
background-color: #f4f4f4;
}
</style>
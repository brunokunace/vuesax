<template lang="html">
  <div
    :style="styleChip"
    :class="[
      `vs-chip-${color}`,
      {
        'closable': closable,
        'con-color': color
      }
    ]"
    class="con-vs-chip">


    <span class="text-chip">
      <slot>
      </slot>
    </span>


    <button
      v-if="closable"
      class="btn-close"
      @click="closeChip">
      <i class="material-icons">
        clear
      </i>
    </button>
  </div>
</template>

<script>
import _color from '../../utils/color.js'

export default {
  name:'VsChip',
  props:{
    item:{
      type:Boolean,
    },
    value:{},
    active:{
      type:Boolean,
      default:true,
    },
    text:{
      type:String,
      default:null,
    },
    closable:{
      type:[Boolean,String],
      default:false,
    },
    color:{
      type:String,
      default:null,
    },
    icon:{
      type:String,
      default:null,
    }
  },
  computed:{
    styleChip () {
      return {
        background: _color.getColor(this.color,1),
        color: this.color?'rgba(255,255,255,.9)':'rgba(0,0,0,.7)'
      }
    },
    eliminado(){
      if(this.item){
        return true
      } else {
        if(this.vsClosable){
          return this.value
        } else {
          return true
        }
      }
    }
  },
  methods:{
    closeChip () {
      this.$emit('input',false)
      this.$emit('click')
    },
    remove(){
      this.$emit('vs-remove', false)
      this.$emit('input', false)
    }
  }
}
</script>

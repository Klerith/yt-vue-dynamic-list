<script setup lang="ts">
import { propsToAttrMap } from '@vue/shared';
import { ref } from 'vue';
/**
 * Listado dinámico
 * límite de 5 elementos
 */
interface Label {
  name: '';
}

const productTags = ref<Label[]>([ { name: '' } ])

const addProductTag = () => {
  if ( productTags.value.length === 5 ) return;

  productTags.value.push({ name: '' });
}


const onSubmit = () => {
  console.log(productTags.value.map( tag => tag.name ))
}

const deleteProductTag = ( index: number ) => {
  if ( productTags.value.length === 1 ) {
    productTags.value = [ { name: '' } ];
    return;
  }

  productTags.value.splice( index, 1 )
}


</script>

<template>
  <h3>Agregar hasta 5 etiquetas</h3>

  <div class="row" v-for="tag, index in productTags">
    
    <button
      @click="deleteProductTag(index)"
      > - </button>

    <input type="text" :placeholder="index.toString()" v-model="tag.name">
    
    <button 
      v-if="index === (productTags.length - 1)"
      @click="addProductTag">
      +
    </button>

  </div>

  <button @click="onSubmit">Submit</button>

</template>

<style scoped>
.row {
  display: flex;
  margin-bottom: 5px;
}

button {
  margin-right: 5px;
  margin-left: 5px;
}
</style>

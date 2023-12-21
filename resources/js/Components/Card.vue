<script setup>
import { inject } from 'vue';


const Color = inject('color')
</script>

<template>
    <div class="card p-3 rounded-lg duration-500" :class="{
        'bg-blue-600' : Color == 'red',
        'bg-blue-800' : Color == 'blue',
        'bg-blue-900' : Color == 'green',
    }">
      <div class="card-header">
        <slot name="header">Default Header</slot>
      </div>
      <div class="card-body">
        <slot name="body">Default Body</slot>
      </div>
      <div class="card-footer">
        <slot name="footer">Default Footer</slot>
      </div>
    </div>
  </template>

  <script>
  export default {
    name: 'Card',
  };
  </script>



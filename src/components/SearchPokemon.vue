<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps(['onSearch']);
const emits = defineEmits();

const searchTerm = ref('');
let searchTimeout;

const handleSearch = () => {
  clearTimeout(searchTimeout);
  searchTimeout = setTimeout(() => {
    emits('search', searchTerm.value);
  }, 300);
};
</script>

<template>
  <input 
    class="c-search" 
    type="search" 
    name="search" 
    placeholder="Search" 
    v-model="searchTerm" 
    @input="handleSearch"
  >
</template>

<style lang="scss">
  .c-search {
    background: transparent;
    border: none;
    border-bottom: 1px solid #A6A6A6;
    margin-bottom: 0.5rem;
    padding-block: 8px;
    width: 100%;
    color: #A6A6A6;

    &:focus-visible {
      outline: none;
    }

    &::placeholder {      
      color: #C0C0C0;
    }
  }
</style>
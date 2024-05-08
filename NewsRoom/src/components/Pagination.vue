<template>
    <div class="pagination">
      <div class="arrow left-arrow">◄</div>
      <div class="page-numbers">
        <div v-for="pageNumber in visiblePageNumbers" :key="pageNumber" class="page-number-box">
          <div class="page-number">{{ pageNumber }}</div>
        </div>
      </div>
      <div class="arrow right-arrow">►</div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  

  const totalPages = ref(57);
  

  const generateVisiblePageNumbers = () => {
    const visiblePages = [];
    const totalVisiblePages = 2; 
    

    for (let i = 1; i <= totalVisiblePages && i <= totalPages.value; i++) {
      visiblePages.push(i);
    }
  

    if (totalPages.value > totalVisiblePages + 1) {
      visiblePages.push('...');
    }
  

    for (let i = 8; i <= 14 && i <= totalPages.value; i++) {
      visiblePages.push(i);
    }
  

    if (totalPages.value > 14) {
      visiblePages.push('...');
    }
  
 
    for (let i = totalPages.value - 1; i <= totalPages.value; i++) {
      visiblePages.push(i);
    }
  
    return visiblePages;
  };
  

  const visiblePageNumbers = generateVisiblePageNumbers();
  </script>
  
  <style scoped>
  .pagination {

    position: fixed;
    bottom: 5px;
    left: 0; /* Set left to 0 */
    width: 100%; /* Make it occupy full width */
    display: flex;
    justify-content: center;
  }
  
  .arrow {
    cursor: pointer;
    padding: 5px;
  }
  
  .page-numbers {
    display: flex;

  }
  
  .page-number-box {
    display:block;
    padding: 10px;
    margin: 0 5px;
    color:black;
    border: 1px solid white;
    background-color: white;
  }
  
  .page-number {
    padding: 5px;
  }
  
  .left-arrow,
  .right-arrow {
    margin: 0 5px;
    border: 1px solid white;
    font-size: 20px;
    background-color: white;
    color:black;
  }
  
  /* Responsive adjustments */
 
  </style>
  
<template>
</template>
  
<script>
  export default {
    name: "Sort",
    methods: {

    getSortFilter(){

        var sortFilter = [];

        sortFilter.push('Trier par date');
        sortFilter.push('Trier par état');
        sortFilter.push('Trier par nom');
        sortFilter.push('Trier par priorité');

        return sortFilter;

    },

    handleItemClick(item) {
        
        if(item === 'Trier par date'){

        }else if(item === 'Trier par état'){
         
        }else if(item === 'Trier par nom'){
          
        }else if(item === 'Trier par priorité'){
          
        }else{
            console.log('error')
        }

      },

    },

  };
  
  </script>
  
  <style scoped>
  
  </style>
  
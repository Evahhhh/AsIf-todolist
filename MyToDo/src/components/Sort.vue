<template>

  <div class="sort">
    <p>Sort by: </p>
    <button v-for = "item in getSortFilter()" :key="item" @click="handleItemClick(item)" class="button" v-on:setSorter="setSorter(item)">
      {{item}}
      
    </button>
  </div>

</template>
  
<script>
  import DisplayList from './DisplayList.vue'

  export default {
    name: "Sort",
    components: {
        DisplayList,
    },
    methods: {

    getSortFilter(){

        var sortFilter = [];

        sortFilter.push('Date');
        sortFilter.push('Name');
        sortFilter.push('Priority');
        sortFilter.push('State');

        return sortFilter;

    },

    handleItemClick(item) {
        
        if(item === 'Date'){

          console.log('Sort by Date');
          this.DisplayList.sortByDate();

        }else if(item === 'Name'){

          console.log('Sort by Name');
          this.DisplayList.sortByName();
         
        }else if(item === 'Priority'){

          console.log('Sort by Priority')
          
        }else if(item === 'State'){

          console.log('Sort by State')
          
        }else{
            console.log('error')
        }

      },

    },

  };
  
  </script>
  
  <style scoped>
  .sort{
    display : flex;
    background-color: white;
    width: 100%;
    padding : 20px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.25);
    gap : 20px;
  }

  button{
    position: relative;
    padding-left: 20px;
    padding: 5px 10px 5px 25px;
    border-radius: 10px;
    border: none;
  }

  button::before {
    content: "";
    position: absolute;
    left: 10px; /* positionner le cercle à 5px de la gauche du bouton */
    top: 50%; /* positionner le cercle verticalement au centre du bouton */
    transform: translate(-50%, -50%); /* centrer le cercle */
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: #ccc;
  }

  button::before:hover {
    background-color: #aaa; /* changer la couleur de fond au survol */
  }

  button:focus::before {
    background-color: #f00; /* changer la couleur de fond lorsque le cercle est sélectionné /
    outline: none; / supprimer le contour par défaut du bouton lorsqu'il est sélectionné */
  }
  
  @media (max-width: 481px){
    .sort{
      position: fixed;
      bottom: 0;
    }
  }
  </style>
  
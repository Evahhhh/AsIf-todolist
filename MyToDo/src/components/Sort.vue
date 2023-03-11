<template>

  <div class="sort">
    <div v-if="displayPC">
      <p>Sort by: </p>
    </div>
      <button v-for = "item in getSortFilter()" :key="item" v-bind:id="item" @click="handleItemClick(item)" class="button" v-on:setSorter="setSorter(item)">
        {{item}}
      </button>
    
  </div>

</template>
  
<script>
  import DisplayList from './DisplayList.vue'
  import {eventBus} from '../event-bus.js';

  export default {
    name: "Sort",
    mounted() {
      window.addEventListener('resize', this.updateDisplayData);
      this.updateDisplayData(); // appeler la méthode pour afficher correctement l'affichage de départ
    },
    destroyed() {
      window.removeEventListener('resize', this.updateDisplayData);
    },
    setup(){
      function handleItemClick(item) {

        document.getElementById(item).style.background="#35D99E";
        document.getElementById(item).style.color="white";
        document.getElementById(item).style.fontWeight = "bold";

      
        if(item === 'Date'){
          eventBus.emit('setSorter', 'date');
          //désactiver les autres boutons
          document.getElementById("Name").style.background="white";
          document.getElementById("Priority").style.background="white";
          document.getElementById("State").style.background="white";

          document.getElementById("Name").style.color="black";
          document.getElementById("Priority").style.color="black";
          document.getElementById("State").style.color="black";

          document.getElementById("Name").style.fontWeight = "normal";
          document.getElementById("Priority").style.fontWeight = "normal";
          document.getElementById("State").style.fontWeight = "normal";
        }else if(item === 'Name'){
          eventBus.emit('setSorter', 'name'); 
          //désactiver les autres boutons
          document.getElementById("Date").style.background="white";
          document.getElementById("Priority").style.background="white";
          document.getElementById("State").style.background="white";

          document.getElementById("Date").style.color="black";
          document.getElementById("Priority").style.color="black";
          document.getElementById("State").style.color="black";

          document.getElementById("Date").style.fontWeight = "normal";
          document.getElementById("Priority").style.fontWeight = "normal";
          document.getElementById("State").style.fontWeight = "normal";
        }else if(item === 'Priority'){
          eventBus.emit('setSorter', 'priority');
          //désactiver les autres boutons
          document.getElementById("Name").style.background="white";
          document.getElementById("Date").style.background="white";
          document.getElementById("State").style.background="white";

          document.getElementById("Name").style.color="black";
          document.getElementById("Date").style.color="black";
          document.getElementById("State").style.color="black";

          document.getElementById("Name").style.fontWeight = "normal";
          document.getElementById("Date").style.fontWeight = "normal";
          document.getElementById("State").style.fontWeight = "normal";
        }else if(item === 'State'){
          eventBus.emit('setSorter', 'state');
          //désactiver les autres boutons
          document.getElementById("Name").style.background="white";
          document.getElementById("Priority").style.background="white";
          document.getElementById("Date").style.background="white";

          document.getElementById("Name").style.color="black";
          document.getElementById("Priority").style.color="black";
          document.getElementById("Date").style.color="black";

          document.getElementById("Name").style.fontWeight = "normal";
          document.getElementById("Priority").style.fontWeight = "normal";
          document.getElementById("Date").style.fontWeight = "normal";
        }else{
            console.log('error')
        }
      }

      return {
        handleItemClick,
      }
    },
    components: {
        DisplayList,
    },
    data() {
      return {
        selectedItem: null,
        isSelected: false,
        displayPC: false,
      }
    },
    methods: {

    getSortFilter(){

        var sortFilter = [];

        sortFilter.push('Name');
        sortFilter.push('Date'); 
        sortFilter.push('State');
        sortFilter.push('Priority');

        return sortFilter;

    },
    updateDisplayData() {
      this.displayPC = window.innerWidth > 480;
    },

    },

  };
  
  </script>
  
  <style scoped>
  .sort{
    display : flex;
    align-items: center;
    background-color: white;
    width: 100%;
    padding : 20px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.25);
    gap : 20px;
  }

  button{
    position: relative;
    padding: 5px 10px 5px 25px;
    border-radius: 10px;
    border: none;
    background-color: white;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.25);
    cursor: pointer;
    transition: box-shadow 0.3s ease-in-out;
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
    transition: background-color 0.3s ease; /* ajouter une transition de 0.3s pour la couleur de fond */
  }

  button:hover{
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
  }
  
  @media (max-width: 481px){
    .sort{
      position: fixed;
      bottom: 0;
      justify-content: center;
    }
  }
  </style>
  
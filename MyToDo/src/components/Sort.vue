<template>

  <div class="sort">
    <!-- Si l'affichage se fait sur PC -->
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
      /**
       * Manages the elements entered in the form and adds the task if they are good
       */
      function handleItemClick(item) {

        document.getElementById(item).style.background="#35D99E";
        document.getElementById(item).style.color="white";
        document.getElementById(item).style.fontWeight = "bold";
      
        if(item === 'Start Date'){
          eventBus.emit('setSorter', 'startDate');
          //désactiver les autres boutons
          this.manageStyle(["Name", "Priority", "State", "End Date"]);

        }else if(item === 'End Date'){
          eventBus.emit('setSorter', 'endDate');
          //désactiver les autres boutons
          this.manageStyle(["Name", "Priority", "State", "Start Date"]);

        }else if(item === 'Name'){
          eventBus.emit('setSorter', 'name'); 
          //désactiver les autres boutons
          this.manageStyle(["Start Date", "Priority", "State", "End Date"]);

        }else if(item === 'Priority'){
          eventBus.emit('setSorter', 'priority');
          //désactiver les autres boutons
          this.manageStyle(["Name", "Start Date", "State", "End Date"]);

        }else if(item === 'State'){
          eventBus.emit('setSorter', 'state');
          //désactiver les autres boutons
          this.manageStyle(["Name", "Priority", "Start Date", "End Date"]);
          
        }else if(item === 'End Date'){
          eventBus.emit('setSorter', 'endDate');
          //désactiver les autres boutons
          this.manageStyle(["Name", "Priority", "State", "Start Date"]);

        }else{
            console.log('error when click on add button')
        }
      }

      /**
       * Changes other buttons style
       */
      function manageStyle(buttons){

        for (var i = 0; i < buttons.length; i++){
          document.getElementById(buttons[i]).style.background="white";
          document.getElementById(buttons[i]).style.color="black";
          document.getElementById(buttons[i]).style.fontWeight = "normal";
        }
      }

      return {
        handleItemClick,
        manageStyle,
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
      /**
       * Return filters
       */
      getSortFilter(){

          var sortFilter = [];

          sortFilter.push('Name');
          sortFilter.push('Start Date'); 
          sortFilter.push('End Date')
          sortFilter.push('State');
          sortFilter.push('Priority');

          return sortFilter;

      },

      /**
       * Manages the size of the user's screen in order to display the right elements live
       */
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
    white-space: nowrap;
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
      padding-left: 220px;
      overflow-x: scroll;
    }
  }
  </style>
  
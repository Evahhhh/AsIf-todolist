<template>

  <!-- PC ET TABLETTE-->
  <body class="pagePC" v-if="displayPC">
      <div class="sidebar" id="sidebar" :class="{ 'hidden': !showSidebar }">
        <img
        alt="Vue logo"
        class="logo"
        src="@/assets/img/logo2.png"
        width="120"
        />
        <NewTask />
      </div>
      <button id="toggleBtn" @click="toggleSidebar" class="toggle-button">
        <img 
        alt="Toggle SideBar button" 
        v-bind:src="imgArrowSrc"
        width="50"
        />
      </button>
      <DisplayList v-if="!displayPC"/>
      <div class="content">
        <Sort />
        <DisplayList v-if="displayPC"/>
      </div>
    </body>


    <!-- TELEPHONE -->
    <body class="pageTEL" v-if="!displayPC">
      <div class="hautPgTel" v-if="!displayPC">
        <div class="sidebar" id="sidebar" :class="{ 'hidden': !showSidebar }">
          <img
          alt="Vue logo"
          class="logo"
          src="@/assets/img/logo2.png"
          width="150"
          />
          <NewTask />
        </div>
        <button id="toggleBtn" @click="toggleSidebar" class="toggle-button">
          <img 
          alt="Toggle SideBar button" 
          v-bind:src="imgArrowSrc"
          width="50"
          />
        </button>
        <DisplayList v-if="!displayPC"/>
      </div>
      <div class="basPgTel" v-if="!displayPC">
        <div class="content">
          <Sort />
          <DisplayList v-if="displayPC"/>
        </div>
      </div>
    </body>
    
</template>

<style scoped>
.pagePC{
  display: flex;
}

.pageTEL{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.sidebar{
  background-color: #34DA9F;
  flex-basis: 35%;
  padding: 20px;
  display : flex;
  align-items: center;
  flex-direction : column;
  gap : 30px;
}

.content{
  flex-basis: 75%;
  padding: 0;
}

.toggle-button{
  background-color: transparent;
  border: none;
  cursor : pointer;

  box-shadow: 5px 5px 21px 5px rgb(0 0 0 / 15%);
  width: 60px;
  height: 60px;
  border-radius: 0px 0px 5px 0px;
  position: relative;
}


/* Téléphone */
@media (max-width: 480px) {
  .hidden {
    display: none;
  }

  .pagePC{
    flex-direction: column;
  }

  .content{
    display : flex;
    flex-direction: column-reverse;
  }
}

/* PC et tablettes */
@media (min-width: 481px){
  .toggle-button{
    visibility: hidden;  
    display : none;
  }
}

</style>

<script>
import Sort from './components/Sort.vue';
import NewTask from './components/NewTask.vue';
import DisplayList from './components/DisplayList.vue';
import arrowDown from "@/assets/icons/down-arrow.png";
import arrowUp from "@/assets/icons/up-arrow.png";

export default {
  mounted() {
    window.addEventListener('resize', this.updateDisplayData);
    this.updateDisplayData(); // appeler la méthode pour afficher correctement l'affichage de départ
  },
  destroyed() {
    window.removeEventListener('resize', this.updateDisplayData);
  },
  components: {
    Sort,
    NewTask,
    DisplayList,
  },

  data() {
    return {
      showSidebar: false,
      imgArrowSrc: arrowDown,
      displayPC: false,
    }
  },
  methods: {
    /**
     * Toggle the sidebar
     */
    toggleSidebar() {
      this.showSidebar = !this.showSidebar;

      if(this.showSidebar == false){
        this.imgArrowSrc = arrowDown
      }else{
        this.imgArrowSrc = arrowUp
      }
    },
    /**
     * Update when user change the screen's size
     */
    updateDisplayData() {
      this.displayPC = window.innerWidth > 480;
    },
  },
};

</script>
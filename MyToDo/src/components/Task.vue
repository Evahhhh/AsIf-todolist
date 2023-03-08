<template>
    <app-accordion class="accordion no-select" >
        <template v-slot:title>
            <div  class="header">
                {{ propTask ? propTask.name : "" }}
                {{ propTask ? propTask.state : "" }}
                {{ propTask ? propTask.prio : "" }}
                <button @click="removeTask" class="removeBtn">
                    <img src="../assets/icons/remove.png" alt="Trash" />
                </button>
            </div>
        </template>

        <template v-slot:content>
            <div  class="content">
                {{ propTask ? propTask.desc : "" }}
                {{ propTask ? propTask.startDate : "" }}
                {{ propTask ? propTask.endDate : "" }}

            </div>
        </template>

    </app-accordion>

</template>


<script>
import AppAccordion from "./Accordion.vue";

export default {
  name: "Task",
  props: {
    propTask: {
      type: Object,
      required: true,
    },
  },
  components: {
    AppAccordion,
  },
  methods:{
    removeTask(){
        //suppresion de la tâche concernée
        console.log("click");
    }
  }
};
</script>


<style scoped>

.no-select{
    user-select: none;
}

.header{
    display: flex;
    align-items : center;
    justify-content: space-between;
}

.removeBtn{
    background-color: transparent;
    border: none;
    cursor : pointer;  
}

img{
    width : 40px;
}

</style>
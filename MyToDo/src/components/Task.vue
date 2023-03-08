<template>
    <app-accordion class="accordion no-select" >
        <template v-slot:title>
            <div  class="header">
                {{ propTask ? propTask.name : "" }}
                <div class="toRight">
                    <State :propTask="propTask" />
                    <Priority :propTask="propTask" />
                    <button @click="removeTask" class="removeBtn">
                        <img src="../assets/icons/remove.png" alt="Trash" />
                    </button>
                </div>
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
import State from "./tag/State.vue";
import Priority from "./tag/Priority.vue";

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
    State,
    Priority,
  },
  methods:{
    removeTask(){
        
        window.localStorage.removeItem(this.propTask.name);
        console.log("click");
        location.reload();
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

.toRight{
    display: flex;
    gap : 10px;
    align-items : center;
}

</style>
<template>
    <app-accordion class="accordion no-select" >
        <template v-slot:title>
            <div  class="header">
                <div class="word-break">
                    {{ propTask ? propTask.name : "" }}
                </div>
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
            <div class="content word-break">
                <p>
                    Description : {{ propTask ? propTask.desc : "" }}
                </p>
                <p>
                    Start date : {{ propTask ? propTask.startDate : "" }}
                </p>
                <p>
                    End date : {{ propTask ? propTask.endDate : "" }}
                </p>

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
    /**
     * Delete the task
     */
    removeTask(){
        window.localStorage.removeItem(this.propTask.name);
        location.reload();
    }
  }
};
</script>


<style scoped>

.content{
    display : flex;
    flex-direction : column;
    gap : 5px;
    padding :5px;
}

.word-break{
    word-break: break-all;
}

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
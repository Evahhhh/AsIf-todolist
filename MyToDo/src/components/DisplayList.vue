<template>

    <div v-if="getList().length > 0">   
        <Task v-for="item in getList()" :key="item.id" :propTask="item"/>
    </div>
    <div class="emptyPage" v-else>
        <h1>
            Nothing to see here... Well, that's odd.
        </h1>
        <img src="../assets/img/noTask.png" alt="Waiting you to add a task" />
        <h2>
            Does your organization suck that much?
        </h2>
    </div>

</template>


<script>
import Task from "./Task.vue";


export default {

    name: "DisplayList",
    components: {
    Task,
    },
    methods: {

        getList(){

            var list = [],
                keys = Object.keys(localStorage),
                i = keys.length;

            while(i--){

                var value = localStorage.getItem(keys[i]);
                value = JSON.parse(value);
                
                list.push(value);

            }

            return list;
            
        },

    },

};

</script>


<style scoped>
.emptyPage{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

img{
    height : 400px;
}


</style>
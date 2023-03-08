<template>
    <Task v-for="item in getList()" :key="item.id" :propTask="item"/>

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

            console.log(list);

            return list;
            
        },

    },

};

</script>


<style scoped>


</style>
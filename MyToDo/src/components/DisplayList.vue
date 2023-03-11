<template>

    <div class="list" v-if="getList().length > 0"> 
        <div class="listSorted" v-if="getSorter() == ''"> 
            <Task v-for="item in getList()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'name'"> 
            <Task v-for="item in sortByName()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'date'"> 
            <Task v-for="item in sortByDate()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'priority'"> 
            <Task v-for="item in sortByPriority()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'state'"> 
            <Task v-for="item in sortByState()" :key="item.id" :propTask="item"/>
        </div>
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
import { onMounted, ref } from "vue";
import Task from "./Task.vue";
import {eventBus} from '../event-bus.js';

export default {

    name: "DisplayList",

    setup(){

        const sorter = ref("");

        const getList = function () {
    
            var list = [],
                keys = Object.keys(localStorage),
                i = keys.length;

            while(i--){

                var value = localStorage.getItem(keys[i]);
                value = JSON.parse(value);
                
                list.push(value);

            }

            return list;
            
        }

        const sortByDate = function () {
            
            var list = getList();

            return list.sort((a, b) => a.startDate.localeCompare(b.startDate));  

        }

        const sortByName = function () {

            var list = getList();

            return list.sort((a, b) => a.name.localeCompare(b.name));

        }

        const sortByPriority = function () {
    
            var list = getList();

            var prioOrder = { 'High': 0, 'Medium': 1, 'Low': 2 };

            return list.sort((a, b) => prioOrder[a.prio] - prioOrder[b.prio]);
        }

        const sortByState = function () {

            var list = getList();

            return list.sort((a, b) => {
                var stateOrder = { 'To Do': 0, 'Doing': 1, 'Done': 2 };
                return stateOrder[a.state] - stateOrder[b.state];
            });

        }

        const getSorter = function () {    
            return sorter.value;
        }   

        const setSorter = function (newSorter) {
    
            if(newSorter == 'name'){
                sorter.value = 'name';
            }
            else if(newSorter == 'date'){
                sorter.value = 'date';
            }
            else if(newSorter == 'priority'){
                sorter.value = 'priority';
            }
            else if(newSorter == 'state'){
                sorter.value = 'state';
            }
            else{
                sorter.value = '';
            }
            // eventBus.emit('setSorter', sorter.value);

        }

        onMounted(() => {
            eventBus.on('setSorter',setSorter);
        });

        return {
            sorter: '',
            getList,
            sortByDate,
            sortByName,
            sortByPriority,
            sortByState,
            getSorter,
            setSorter,
        };
    },
    components: {
        Task,
    },

};

</script>


<style scoped>
.emptyPage{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding : 20px;
}

img{
    height : 400px;
}

/* Téléphone */
@media (max-width: 480px) {
    img{
        height : 300px;
    }

    .list,
    .emptyPage{
        padding-bottom : 80px;
    }
}


</style>
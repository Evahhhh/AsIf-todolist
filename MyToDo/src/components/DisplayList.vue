<template>
    <!-- Displaying the task list according to the type of sorting -->
    <div class="list" v-if="getList().length > 0"> 
        <div class="listSorted" v-if="getSorter() == ''"> 
            <Task v-for="item in getList()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'name'"> 
            <Task v-for="item in sortByName()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'startDate'"> 
            <Task v-for="item in sortByStartDate()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'endDate'"> 
            <Task v-for="item in sortByEndDate()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'priority'"> 
            <Task v-for="item in sortByPriority()" :key="item.id" :propTask="item"/>
        </div>
        <div class="listSorted" v-else-if="getSorter() == 'state'"> 
            <Task v-for="item in sortByState()" :key="item.id" :propTask="item"/>
        </div>
    </div>
    
    <!-- If the page is empty, we display an image and its description  -->
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

        /**
         * Returns the list of all tasks stored in the user's browser
         */
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

        /**
         * Returns the list of tasks sorted by start date
         */
        const sortByStartDate = function () {
            
            var list = getList();

            return list.sort((a, b) => a.startDate.localeCompare(b.startDate));  

        }

        /**
         * Returns the list of tasks sorted by start date
         */
         const sortByEndDate = function () {
            
            var list = getList();

            return list.sort((a, b) => a.endDate.localeCompare(b.endDate));  

        }

        /**
         * Returns the list of tasks sorted by name
         */
        const sortByName = function () {

            var list = getList();

            return list.sort((a, b) => a.name.localeCompare(b.name));

        }

        /**
         * Returns the list of tasks sorted by priority
         */
        const sortByPriority = function () {
    
            var list = getList();

            var prioOrder = { 'High': 0, 'Medium': 1, 'Low': 2 };

            return list.sort((a, b) => prioOrder[a.prio] - prioOrder[b.prio]);
        }

        /**
         * Returns the list of tasks sorted by state
         */
        const sortByState = function () {

            var list = getList();

            return list.sort((a, b) => {
                var stateOrder = { 'To Do': 0, 'Doing': 1, 'Done': 2 };
                return stateOrder[a.state] - stateOrder[b.state];
            });

        }

        /**
         * Returns the current sorting method
         */
        const getSorter = function () {    
            return sorter.value;
        }   

        /**
         * Sets the sorting method
         * @param {string} newSorter 
         */
        const setSorter = function (newSorter) {
    
            if(newSorter == 'name'){
                sorter.value = 'name';
            }
            else if(newSorter == 'startDate'){
                sorter.value = 'startDate';
            }else if(newSorter == 'endDate'){
                sorter.value = 'endDate';
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
        }

        onMounted(() => {
            eventBus.on('setSorter',setSorter);
        });

        return {
            sorter: '',
            getList,
            sortByStartDate,
            sortByEndDate,
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
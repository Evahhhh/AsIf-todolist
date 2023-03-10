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
            <Task v-for="item in sortByStatus()" :key="item.id" :propTask="item"/>
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
import Task from "./Task.vue";


export default {

    name: "DisplayList",
    data() {
        return {
            sorter: '',
        };
    },
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

        sortByDate(){

            var list = getList();

            return list.sort((a, b) => a.startDate.localeCompare(b.startDate));

        },

        sortByName(){

            var list = getList();

            return list.sort((a, b) => a.name.localeCompare(b.name));

        },

        sortByPriority(){

            var list = getList();

            return list.sort((a, b) => a.prio.localeCompare(b.prio));

        },

        sortByState(){

            var list = getList();

            return list.sort((a, b) => a.state.localeCompare(b.state));

        },

        getSorter(){

            return this.sorter;

        },

        setSorter(newSorter){
            this.$emit("setSorter")

            if(newSorter == 'name'){
                this.sorter = 'name';
            }
            else if(newSorter == 'date'){
                this.sorter = 'date';
            }
            else if(newSorter == 'priority'){
                this.sorter = 'priority';
            }
            else if(newSorter == 'state'){
                this.sorter = 'state';
            }
            else{
                this.sorter = '';
            }


        }

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
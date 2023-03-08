<template>
    <div class="prio" :style="{ backgroundColor: getColor() }">
        {{ propTask ? propTask.prio : "" }}
    </div>
</template>

<script>
export default{
    name : "Priority",
    props: {
        propTask: {
            type: Object,
            required: true,
        },
    },
    methods : {
        getColor(){
            if(this.propTask.prio === 'High'){
                return '#990D35';
            }else if(this.propTask.prio === 'Medium'){
                return '#FFB627';
            }else if(this.propTask.prio === 'Low'){
                return '#31D198';
            }else{
                return '#31D198';
            }
        },
    },
};

</script>

<style>
.prio{
    color : white;
    padding : 2px 10px;
    border-radius : 5px;
}
</style>
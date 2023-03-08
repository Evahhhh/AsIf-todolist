<template>
    <div class="state" :style="{ backgroundColor: getColor() }">
        {{ propTask ? propTask.state : "" }}
    </div>
</template>

<script>
export default{
    name : "State",
    props: {
        propTask: {
            type: Object,
            required: true,
        },
    },
    methods : {
        getColor(){
            if(this.propTask.state === 'To Do'){
                return '#990D35';
            }else if(this.propTask.state === 'Doing'){
                return '#FFB627';
            }else if(this.propTask.state === 'Done'){
                return '#31D198';
            }else{
                return '#31D198';
            }
        },
    },
};

</script>

<style>
.state{
    color : white;
    padding : 2px 10px;
    border-radius : 5px;
}
</style>
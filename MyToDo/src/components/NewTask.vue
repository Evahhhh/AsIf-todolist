 <template>
    <div class="form">
        <h1>New Task</h1>
        <form id="newTask" class="newTask" action="">
            <section>
                <label for="name">Name :</label>
                <input type="text" name="Nom de la tache" placeholder="Dishes" id="name" required/>
            </section>
            <section>
                <label for="desc">Description :</label>
                <input type="text" name="Description" placeholder="Dishes a very bad joke" id="desc" required/>
            </section>
            <div class="doubleSection">
                <section>
                    <label for="startDate">Beginning :</label>
                    <input type="date" name="Date de début" placeholder="01/03/2023" id="startDate" required/>
                </section>
                <section>
                    <label for="endDate">End :</label>
                    <input type="date" name="Date de fin" placeholder="01/03/2023" id="endDate" required/>
                </section>
            </div>
            <section>
                <label for="state">Task State:</label>
                <input list="states" name="state" id="state" required>
                <datalist id="states">
                    <option value="To Do"></option>
                    <option value="Doing"></option>
                    <option value="Done"></option>
                </datalist>
            </section>
            <section>
                <label for="prio">Priority :</label>
                <input list="priorities" name="priority" id="prio" required>
                <datalist id="priorities">
                    <option value="High"></option>
                    <option value="Medium"></option>
                    <option value="Low"></option>
                </datalist>
            </section>
    
            <button id="submitBtn" class="btn" type="button" name="send" @click="handleClick">Add</button>

        </form>

    </div>
</template>

<style scoped>
.form{
    background-color: #f8f8f8;
    box-shadow : 5px 5px 21px 5px rgba(0,0,0,0.15);
    display: flex;
    flex-direction: column;
    width : 90%;
    border-radius : 5px;
    padding : 20px;
}

section{
    display : flex;
    flex-direction : column;
    margin-top : 15px;
}

.doubleSection{
    display : flex;
    justify-content : space-between;
}

.btn{
    border-radius : 5px;
    color : black;
    background-color : white;
    border: none;
    width : 125px;
    padding : 10px 30px;
    cursor : pointer;
    margin: 20px auto 0px auto;
    display: block;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.25);
    transition: box-shadow 0.3s ease-in-out;
}

.btn:hover{
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
}

h1{
    font-size : 25px;
    margin-bottom : -10px;
    text-align: center;
}

input{
    border : solid 1px #34DA9F;
    border-radius : 5px;
    padding : 5px;
}


</style>

<script>
    export default{
        name: "NewTask",
        methods: {

            handleClick(){
                
                const nomInput = document.querySelector('#name');
                const descInput = document.querySelector('#desc');
                const startDateInput = document.querySelector('#startDate');
                const endDateInput = document.querySelector('#endDate');
                const stateInput = document.querySelector('#state');
                const prioInput = document.querySelector('#prio');
                
                if (!nomInput.value || !descInput.value || !startDateInput.value || !endDateInput.value || !stateInput.value || !prioInput.value) {
                    alert('Veuillez remplir tous les champs !');
                }else{
                    
                    if(startDateInput.value > endDateInput.value){
                        alert('La date de début doit être antérieure à la date de fin !');
                    }else{

                        if(stateInput.value != "To Do" && stateInput.value != "Doing" && stateInput.value != "Done"){
                            alert('Veuillez choisir un état valide !');
                        }else{

                            if(prioInput.value != "High" && prioInput.value != "Medium" && prioInput.value != "Low"){
                                alert('Veuillez choisir une priorité valide !');
                            }else{
                                
                                var form = document.getElementById('newTask');
                                var button = document.getElementById('submitBtn');
                                
                                var name = document.getElementById('name').value;
                                
                                var infos = {
                                    name : document.getElementById('name').value,
                                    desc : document.getElementById('desc').value,
                                    startDate : document.getElementById('startDate').value,
                                    endDate : document.getElementById('endDate').value,
                                    state : document.getElementById('state').value,
                                    prio : document.getElementById('prio').value,
                                }
                                
                                window.localStorage.setItem(name, JSON.stringify(infos));                    
                                location.reload();

                            }
                        }

                    }
                
                }
                
            },
        },
    };
    
</script>
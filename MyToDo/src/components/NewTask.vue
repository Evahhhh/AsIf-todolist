<template>
    <div class="form">
        <h1>Nouvelle tâche</h1>
        <form id="newTask" class="newTask" action="">
            <section>
                <label for="name">Nom :</label><br>
                <input type="text" name="Nom de la tache" placeholder="Vaisselle" id="name" required/><br>
            </section>
            <section>
                <label for="desc">Description :</label><br>
                <input type="text" name="Description" placeholder="Faire la vaisselle" id="desc" required/><br>
            </section>
            <section>
                <label for="startDate">Date de Début :</label><br>
                <input type="date" name="Date de début" placeholder="01/03/2023" id="startDate" required/><br>
            </section>
            <section>
                <label for="endDate">Date de Fin :</label><br>
                <input type="date" name="Date de fin" placeholder="01/03/2023" id="endDate" required/><br>
            </section>
            <section>
                <label for="state">État de la tâche:</label><br>
                <input list="states" name="state" id="state" required>
                <datalist id="states">
                    <option value="A faire"></option>
                    <option value="En cours"></option>
                    <option value="Terminé"></option>
                </datalist><br>
            </section>
            <section>
                <label for="prio">Priorité de la tache :</label><br>
                <input list="priorities" name="priority" id="prio" required><br>
                <datalist id="priorities">
                    <option value="Haute"></option>
                    <option value="Moyenne"></option>
                    <option value="Basse"></option>
                </datalist>
            </section>
    
            <button id="submitBtn" class="btn" type="button" name="send" @click="handleClick">Envoyer</button><br>

        </form>

    </div>
</template>

<style scoped>
.form{
    background-color: #f8f8f8;
    box-shadow : 5px 5px 21px 5px rgba(0,0,0,0.15);
    display: flex;
    flex-direction: column;
    padding: 10px;
    width : 300px;
    border-radius : 5px;
}

section{
    margin-top : 15px;
}

.btn{
    margin-top : 15px;
    border-radius : 5px;
    color : black;
    background-color : white;
    border-color: #34DA9F;
    width : 125px;
    padding : 5px;

    margin: 15px auto 0;
    display: block;
}

h1{
    font-size : 25px;
    margin-bottom : -10px;
    text-align: center;
}
</style>

<script>
    export default{
        name: "NewTask",
        methods: {

            handleClick(){

                var form = document.getElementById('newTask');
                var button = document.getElementById('submitBtn');

                console.log(form);
                console.log(button);

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

                var message = "La tâche \'" + name + "\' a bien été ajoutée !";

                alert(message);
                
            },
        },
    };
    
</script>
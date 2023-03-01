<template>
    <div class="form">
        <h1 class="centered">Nouvelle tâche</h1>
        <form id="newTask" action="task">
            <section>
                <label for="name">Nom :</label><br>
                <input type="text" name="Nom de la tache" placeholder="Vaisselle" id="name" required/><br>
            </section>
            <section>
                <label for="desc">Description :</label>
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
                <label for="state">État de la tâche:</label>
                <input list="states" name="state" id="state" required>
                <datalist id="states">
                    <option value="To Do"></option>
                    <option value="Doing"></option>
                    <option value="Done"></option>
                </datalist><br>
            </section>
            <section>
                <label for="prio">Priorité de la tache :</label>
                <input list="priorities" name="priority" id="prio" required><br>
                <datalist id="priorities">
                    <option value="Haute"></option>
                    <option value="Moyenne"></option>
                    <option value="Basse"></option>
                </datalist>
            </section>
    
            <input class="btn centered" type="submit" name="send" value="Envoyer"><br>

            <!-- mettre un @submit.prevent=method au type pour éviter de refresh la page 
            method représente la méthode à coder où l'on récupérera les infos du form
            -->
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
    border-radius : 5px;
}

/* .centered{
    display: flex;
    justify-content: center;
    align-items: center;
} */

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
    // import VCalendar from 'v-calendar';

    // // Use plugin with defaults
    // app.use(VCalendar, {})
</script>
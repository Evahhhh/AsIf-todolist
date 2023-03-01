<template>
    <body>
        <h1>Nouvelle Tâche</h1>
        <h2>Informations Générales</h2>
        <form action="">
            
            <label for="name">Nom de la tache: </label>
            <input type="text" name="Nom de la tâche" placeholder="Vaisselle" id="name" required/><br>
            
            <label for="desc">Description</label>
            <input type="text" name="Description" placeholder="Faire la vaisselle" id="desc" required/><br>
            
            <label for="startDate">Date de Début</label>
            <input type="text" name="Date de début" placeholder="01/03/2023" id="startDate" required/><br>
            
            <label for="endDate">Date de Fin</label>
            <input type="text" name="Date de fin" placeholder="01/03/2023" id="endDate" required/><br>

            <label for="state">État de la tache:</label>
            <input list="states" name="state" id="state" required>
            <datalist id="states">
                <option value="To Do"></option>
                <option value="Doing"></option>
                <option value="Done"></option>
            </datalist><br>

            <label for="prio">Priorité de la tache:</label>
            <input list="priorities" name="priority" id="prio" required>
            <datalist id="priorities">
                <option value="Haute"></option>
                <option value="Moyenne"></option>
                <option value="Basse"></option>
            </datalist>
        </form>
    </body>
</template>
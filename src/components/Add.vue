<template>
    <div class="add-container">
        <h3>Ajouter des notes</h3>
        <input id="branche"   type="text"   placeholder="Branche">
        <input id="examen"    type="text"   placeholder="Nom de l'epreuve">
        <input id="date"      type="date"   placeholder="Date">
        <input id="note"      type="number" placeholder="Note">
        <br>
        <input id="nom"       type="text"   placeholder="Nom">
        <input id="prenom"    type="text"   placeholder="Prénom">
        <input id="prof"      type="text"   placeholder="Prof">
        <input id="classe"    type="text"   placeholder="Classe">
        <br>
        <div class="center">
          <button v-on:click="created()">Ajouter une note</button>
          <p id="status"></p>
        </div>
    </div>
</template>
<script>
  const axios = require('axios');
  export default {
    name: 'Add',
    data() {
      return {
        add: null,
       
      };
    },
    methods: {
      say: function (message) {
        alert(message)
      },
      created: function () {
      // declaration des variables du fromulaire 
      let nom = document.getElementById("nom").value; 
      let prenom = document.getElementById("prenom").value;
      //ici on prend les 4 premiere lettres du nom et du prenom et on les combine pour en faire le visa
      let visa = prenom.substring(0,4)+nom.substring(0,4);  
      // et ici on recupere le données entrées par l utilisateur et on les mets au format JSON
      let data = {  
          "prenom" : prenom,
          "nom"    : nom,
          "visa"   : visa.toLowerCase(),
          "date"   : document.getElementById("date").value,
          "examen" : document.getElementById("examen").value,
          "branche": document.getElementById("branche").value,
          "note"   : document.getElementById("note").value,
          "prof"   : document.getElementById("prof").value,
          "classe" : document.getElementById("classe").value,
          "ecole"  : "eptm"
      }

      let s = [ "Attention le nom, prenom note et le nom de l'exmen sont vides ou la note ne corespond pas au critére,  l'epreuve n'a pas été ajoutée",
                "Les données on bien été ajoutées"];
      //verifaication que le nom et le prenom ne sois pas vide 
      if(prenom == ""  | nom == ""  | data.note == "" | data.examen == "" | data.note > 6 | data.note < 0){
        console.warn(s[0])
        document.getElementById("status").innerHTML = s[0]
      }else{
        console.log(s[1])
        axios.post('http://localhost:3000/addEntry',data)
          .then(res => {
            console.log(res.data);
            document.getElementById("status").innerHTML = res.data;
          }).catch(err => {
            console.log(err.data);
            document.getElementById("status").innerHTML = err.data;
          })
        }
      }
    }
  }
  
</script>
<style>
.add-container {
  text-align: left;
  background-color: rgb(229, 245, 199);
  border-radius: 10px;
  padding-top: 10px;
  padding-left: 25px;
  padding-bottom: 25px;
}

.add-container >.center> button {
  /* size */
  margin-top:20px;
  padding:13px;
  /* style */
  border: none;
  background-color:#04AA6D;
  color:white;
  font-size:17px
}

.add-container >.center> button:hover {
  /* style */
  border-color : #04AA6D;
  background-color:white;
  color:#04AA6D;
}

.center {
  text-align: center;
}

input, select {
  width: 24%;
  padding: 12px 12px;
  margin: 2px;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type=date]{
  padding:9.5px;
}

</style>
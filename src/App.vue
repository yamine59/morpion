<template>
  <div v-if="gagnant" class="resultat">
    <div> Le gagnant est {{ gagnant }}</div>
    <div class="btt" @click="relance" @keydown="key">nouvelle partie</div>
  </div>
  <nav>
    <h1 class="title">
      Morpion
    </h1>
  </nav>

  <div class="morpion">
    <div class="box" @click="boxselected(1)" @keydown="key">{{ note[1] }}</div>
    <div class="box" @click="boxselected(0)" @keydown="key">{{ note[0] }}</div>
    <div class="box" @click="boxselected(2)" @keydown="key">{{ note[2] }}</div>
    <div class="box" @click="boxselected(3)" @keydown="key">{{ note[3] }}</div>
    <div class="box" @click="boxselected(4)" @keydown="key">{{ note[4] }}</div>
    <div class="box" @click="boxselected(5)" @keydown="key">{{ note[5] }}</div>
    <div class="box" @click="boxselected(6)" @keydown="key">{{ note[6] }}</div>
    <div class="box" @click="boxselected(7)" @keydown="key">{{ note[7] }}</div>
    <div class="box" @click="boxselected(8)" @keydown="key">{{ note[8] }}</div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const note = ref(['', '', '', '', '', '', '', '', '']);
const result = ref([
  [0, 1, 2], // Ligne 1 horizontale
  [3, 4, 5], // Ligne 2 horizontale
  [6, 7, 8], // Ligne 3 horizontale
  [0, 3, 6], // Colonne 1 verticale
  [1, 4, 7], // Colonne 2 verticale
  [2, 5, 8], // Colonne 3 verticale
  [0, 4, 8], // Diagonale principale
  [2, 4, 6], // Diagonale secondaire
]);

const notetotal = ['X', 'O'];
const nbn = ref(0);
const noteDejaSelectionner = ref([]);
const gagnant = ref(null);

const boxselected = (n) => {
  // Vérifiez si la case est déjà sélectionnée
  if (noteDejaSelectionner.value.includes(n)) {
    return;
  }

  // Ajoutez la case sélectionnée et mettez à jour le plateau
  noteDejaSelectionner.value.push(n);
  const nouvelleNote = notetotal[nbn.value];
  note.value.splice(n, 1, nouvelleNote);

  // Vérifiez si un joueur a gagné
  const isGagnant = result.value.some(([a, b, c]) => {
    if (note.value[a] && note.value[a] === note.value[b] && note.value[a] === note.value[c]) {
      gagnant.value = note.value[a];
      return true;
    }
    return false;
  });

  if (isGagnant) return;

  // Changement de joueur
  nbn.value = nbn.value === 1 ? 0 : 1;
};

// Fonction pour relancer le jeu
const relance = () => {
  note.value = ['', '', '', '', '', '', '', '', ''];
  noteDejaSelectionner.value = [];
  nbn.value = 0;
  gagnant.value = null;
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

.resultat {
  display: flex;
  position: absolute;
  top: 20%;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: rgba(0, 0, 0, 0.74);
  width: 100vw;
  height: 100px;
  margin: 0;
  padding: 100px;
  gap: 20px;
  color: whitesmoke;
  font-size: large;
  font-family: cursive;
}

nav {
  display: flex;
  justify-content: center;

  .title {
    color: black;
    margin-top: 50px;
    font-size: xx-large;
    font-family: cursive;
  }
}

.morpion {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  width: 330px;
  justify-content: center;
  margin: auto;
  margin-top: 100px;

  .box {
    height: 100px;
    width: 100px;
    background-color: rgb(184, 184, 184);
    margin: 5px;
    cursor: pointer;
    text-align: center;
    align-content: center;
    font-size: xx-large;
    font-family: cursive;
    font-weight: 700;
    color: rgba(255, 255, 255, 0.849);
  }

}

.btt {
  justify-content: center;
  align-items: center;
  cursor: pointer;
  margin: 10px;
  padding: 10px;
  border-radius: 15px;
  background-color: whitesmoke;
  color: black;
}
</style>

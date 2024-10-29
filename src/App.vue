<template>

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
  <button class="btt" @click="relance">nouvelle partie</button>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const note = ref(['x', '', '', '', '', '', '', '', '']);

const result = ref([
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6],
]);

const notetotal = ['X', 'O'];
const nbn = ref(0);
const noteDejaSelectionner = ref([]);

const boxselected = (n) => {
  // for (const [a, b, c] of result.value) {
  //   if ([a]) {
  //     if ([a] === [b] === [c]) {
  //       alert('test');
  //     }
  //   }
  // }

  result.value.forEach((e) => {
    console.log(e);
    const a = e[0];
    const b = e[1];
    const c = e[2];
  });
  if (noteDejaSelectionner.value.includes(n)) {
    return;
  }
  noteDejaSelectionner.value.push(n);
  const nouvelleNote = notetotal[nbn.value];
  note.value.splice(n, 1, nouvelleNote);
  note[n] = notetotal[nbn];
  console.log(note.value);
  if (nbn.value === 1) {
    nbn.value = 0;
    return;
  }
  nbn.value += 1;
  console.log(nbn.value);
};

const relance = () => {
  note.value = ['', '', '', '', '', '', '', '', ''];
  noteDejaSelectionner.value = [];
  nbn.value = 0;
};
</script>

<style>
* {
  box-sizing: border-box;
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
  display: flex;
  margin: auto;
  margin-top: 100px;
  width: 150px;
  height: 50px;
  justify-content: center;
  align-items: center;

}
</style>

<script setup>
import { ref } from 'vue'

let arr1 = ref([[], [], [], [], [], [], [], [], [], [], []])
for (let a = 0; a < 11; a++) {
  for (let b = 1; b < 25; b++) {
    arr1.value[a].push(Math.floor(Math.random() * 9 + 1))
  }
}
let arr2 = ref([])
let count = ref(0)

const add = (n, m) => {
  const num = arr1.value[n * 3 - m].shift()
  arr2.value.push(num)

  if (arr2.value.filter((i) => i === num).length === 3) {
    arr2.value = arr2.value.filter((ii) => ii != num)
    count.value += 1
    if (count.value == 30) {
      alert('恭喜你大获全胜')
      location.reload()
    }
  }
  if (arr2.value.length > 6) {
    alert('很可惜,游戏结束')
    location.reload()
  }
  // console.log(arr2)
}
</script>

<template>
  <h1>高枕枕游戏仿写</h1>
  <table id="table1">
    <thead>
      <tr>
        <th colspan="3">数了个数</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="n in 3">
        <td v-for="m in 3">
          <button @click="add(n, m)">
            {{ arr1[n * 3 - m][0] }}
            <span>/{{ arr1[n * 3 - m][1] }}</span>
          </button>
        </td>
      </tr>
      <tr>
        <td>
          <button @click="add(4, 3)">{{ arr1[9][0] }}</button>
        </td>
        <td id="count">{{ count }}/30</td>
        <td>
          <button @click="add(4, 2)">{{ arr1[10][0] }}</button>
        </td>
      </tr>
    </tbody>
  </table>
  <br /><br /><br />
  <table id="table2">
    <tbody>
      <td v-for="i in 7">{{ arr2[i - 1] }}</td>
    </tbody>
  </table>
</template>

<style scoped>
h1 {
  text-align: center;
  color: skyblue;
}

#table1 {
  margin: auto;
  width: 250px;
  height: 300px;
  text-align: center;
}

#table2 td {
  border: 1px solid #333;
  border-radius: 20%;
}

thead,
tfoot {
  background-color: skyblue;
  /* color: #fff; */
}

#count {
  border: none;
  color: #ff4e6a;
}

#table2 {
  margin: auto;
  text-align: center;
}
#table2 td {
  width: 50px;
  height: 50px;
  font: 30px bold;
}

button {
  border-radius: 20%;
  border: none;
  opacity: 0.9;
  background: #1a1a1a;
  box-shadow: 0 2px 12px #1a1a1a;
  color: white;
  width: 60px;
  height: 60px;
  /* font-size: 22px; */
  font: 22px bold;
}

button:hover {
  opacity: 1;
}

button:active {
  box-shadow: none;
}

button span {
  font-size: 8px;
}
</style>

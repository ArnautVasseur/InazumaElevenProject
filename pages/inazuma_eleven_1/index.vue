<template>
    <div class="header">        
        <comp_header/>
    </div>
    <main>
        <div class="container">
            <div class="leftspace"></div>
            <div class="table">
                <div class="filters">
                    <input v-model="filters.fullName" placeholder="Full Name" />
                    <input v-model="filters.nickName" placeholder="Nick Name" />
                    <select v-model="filters.position" placeholder="Position">
                        <option value="GoalKeeper">GoalKeeper</option>
                        <option value="Defender">Defender</option>
                        <option value="Midfielder">Midfielder</option>
                        <option value="Forward">Forward</option>
                    </select>
                    <input v-model="filters.gender" placeholder="Gender" />
                    <input v-model="filters.size" placeholder="Size" />
                    <input v-model="filters.element" placeholder="Element" />
                </div>

                <table>
                    <thead>
                        <tr>
                            <th @click="sortBy('fullname')">Full Name</th>
                            <th @click="sortBy('nickname')">Nickname</th>
                            <th @click="sortBy('position')">Position</th>
                            <th @click="sortBy('gender')">Gender</th>
                            <th @click="sortBy('size')">Size</th>
                            <th @click="sortBy('element')">Element</th>
                            <th @click="sortBy('fp')">FP</th>
                            <th @click="sortBy('tp')">TP</th>
                            <th @click="sortBy('kick')">Kick</th>
                            <th @click="sortBy('body')">Body</th>
                            <th @click="sortBy('control')">Control</th>
                            <th @click="sortBy('guard')">Guard</th>
                            <th @click="sortBy('speed')">Speed</th>
                            <th @click="sortBy('stamina')">Stamina</th>
                            <th @click="sortBy('guts')">Guts</th>
                            <th @click="sortBy('freedom')">Freedom</th>
                        </tr>
                    </thead>

                    <tbody>
                        <tr v-for="player in filteredPlayers" :key="player.player_id">
                            <td>{{ player.fullname }}</td>
                            <td>{{ player.nickname }}</td>
                            <td>{{ player.position }}</td>
                            <td>{{ player.gender }}</td>
                            <td>{{ player.size }}</td>
                            <td>{{ player.element }}</td>
                            <td>{{ player.fp }}</td>
                            <td>{{ player.tp }}</td>
                            <td>{{ player.kick }}</td>
                            <td>{{ player.body }}</td>
                            <td>{{ player.control }}</td>
                            <td>{{ player.guard }}</td>
                            <td>{{ player.speed }}</td>
                            <td>{{ player.stamina }}</td>
                            <td>{{ player.guts }}</td>
                            <td>{{ player.freedom }}</td>
                        </tr>
                    </tbody>

                </table>
            </div>
        </div>
    </main>
</template>

<script setup>

import { API } from "../../utils/axios"

let players = ref([]);
let filters = reactive({
    fullName: "",
    nickName: "",
    position: "",
    gender: "",
    size: "",
    element: ""
});

const getPlayers = async () => {
    const response = await API.get(`/players_ie1`)
    players.value = response.data
}

onMounted(async () => {
    await getPlayers()
})

const filteredPlayers = computed(() => {
  return players.value.filter((player) => {
    // Customize the filtering logic for each column
    return (
      player.fullname.toLowerCase().includes(filters.fullName.toLowerCase())
      // Add similar conditions for other columns
    );
  });
});

const sortOrders = {};

const sortBy = (column) => {
  if (!sortOrders[column]) {
    sortOrders[column] = 1;
  } else {
    sortOrders[column] *= -1;
  }

  players.value.sort((a, b) => {
    const valueA = a[column];
    const valueB = b[column];

    if (typeof valueA === "string" && typeof valueB === "string") {
      return sortOrders[column] * valueA.localeCompare(valueB);
    } else if (typeof valueA === "number" && typeof valueB === "number") {
      return sortOrders[column] * (valueA - valueB);
    } else {
      return 0;
    }
  });
};

</script>

<style lang="scss" scoped>

.header{
    margin-left: 20px;
    margin-top: 15px;
    width: 300px;
    height: 95vh;
    position: fixed;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.container{
    display: flex;
}

.leftspace{
    width: 23%;
}

main{
    color: white;
    font-family: $NotoSans, "sans-serif";
    padding: 50px;
}

table {
    border-collapse: collapse;
    width: 100%;
}

th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: center;
}

th {
    cursor: pointer;
}

thead tr th{
    background: rgb(107, 133, 252);
    color: black;
    border: white 1px solid;
}

.filters{
    display: flex;
    gap: 50px;
    margin-bottom: 50px;

    input{
        background: none;
        border: 1px solid white;
        color: white;
        padding: 15px;
    }
}

::placeholder{
    color: #b0b0b0;
}

select{
    all: unset;
    border: 2px solid white;
    font-size: 18px;
    color: white;
    background-color: $primary-color;
}

</style>
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
                        <option value="" disabled selected="selected">Position</option>
                        <option value="GK">Goakeeper</option>
                        <option value="DF">Defender</option>
                        <option value="MF">Midfielder</option>
                        <option value="FW">Forward</option>
                    </select>
                    <select v-model="filters.gender" placeholder="Gender">
                        <option value="" disabled selected="selected">Gender</option>
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                    </select>
                    <select v-model="filters.size" placeholder="Size">
                        <option value="" disabled selected="selected">Size</option>
                        <option value="Small">Small</option>
                        <option value="Medium">Medium</option>
                        <option value="Large">Large</option>
                    </select>
                    <select v-model="filters.element" placeholder="Element">
                        <option value="" disabled selected="selected">Element</option>
                        <option value="Air">Air</option>
                        <option value="Earth">Earth</option>
                        <option value="Fire">Fire</option>
                        <option value="Wood">Wood</option>
                    </select>
                </div>

                <comp_button class="reset" @click="resetFilters()">
                    Reset all filters
                </comp_button>

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
                            <td :class="{ 'GK': player.position === 'GK', 'DF': player.position === 'DF', 'MF': player.position === 'MF', 'FW': player.position === 'FW' }">{{ player.position }}</td>
                            <td :class="{ 'male': player.gender === 'Male', 'female': player.gender === 'Female' }">{{ player.gender }}</td>
                            <td>{{ player.size }}</td>
                            <td :class="{ 'earth': player.element === 'Earth', 'air': player.element === 'Air', 'fire': player.element === 'Fire', 'wood': player.element === 'Wood' }">{{ player.element }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.fp / 2) / 100})` }">{{ player.fp }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.tp / 2) / 100})` }">{{ player.tp }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.kick / 1.3) / 100})` }">{{ player.kick }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.body / 1.3) / 100})` }">{{ player.body }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.control / 1.3) / 100})` }">{{ player.control }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.guard / 1.3) / 100})` }">{{ player.guard }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.speed / 1.3) / 100})` }">{{ player.speed }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.stamina / 1.3) / 100})` }">{{ player.stamina }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.guts / 1.3) / 100})` }">{{ player.guts }}</td>
                            <td :style="{ 'background': `rgba(0, 127.5, 255, ${(player.freedom * 2) / 100})` }">{{ player.freedom }}</td>
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
    return (
        player.fullname.toLowerCase().includes(filters.fullName.toLowerCase()) &&
        player.nickname.toLowerCase().includes(filters.nickName.toLowerCase()) &&
        player.position.includes(filters.position) &&
        player.gender.includes(filters.gender) &&
        player.size.includes(filters.size) &&
        player.element.includes(filters.element)
    );
  });
});

const resetFilters = () => {
    filters.fullName = "",
    filters.nickName = "",
    filters.position = "",
    filters.gender = "",
    filters.size = "",
    filters.element = "";
}
    

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
    width: 26%;
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
    border: 1px solid white;
    color: white;
    background-color: $primary-color;
    font-size: 1rem;
    text-indent: 5px;
    width: 100%;
}

.reset{
    margin: 30px 0px;
}

.earth {
  background-color: rgba(120, 74, 74);
}

.air {
  background-color: rgb(33, 80, 143);
}

.fire {
  background-color: rgb(234, 50, 50);
}

.wood {
  background-color: rgb(35, 74, 44);
}

.male{
    color: rgb(85, 85, 255);
}

.female{
    color: rgb(225, 124, 218);
}

.GK{
    color: #806767;
}

.DF{
    color: #2b6332;
}

.MF{
    color: #373fca;
}

.FW{
    color: #d33131;
}

</style>
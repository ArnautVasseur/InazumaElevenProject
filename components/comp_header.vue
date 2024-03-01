<template>
    <div class="header">
        <ul>
            <p>Inazuma Eleven 1</p>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Players Stats</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Moves</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Recruitment</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Cheats</RouterLink>
            </li>
        </ul>
        <ul>
            <p>Inazuma Eleven 2</p>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Players Stats</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Moves</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Recruitment</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Cheats</RouterLink>
            </li>
        </ul>
        <ul>
            <p>Inazuma Eleven 3</p>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Players Stats</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Moves</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Recruitment</RouterLink>
            </li>
            <li>
                <RouterLink to="/inazuma_eleven_1/">Cheats</RouterLink>
            </li>
        </ul>
    </div>
</template>

<script>

</script>

<style lang="scss" scoped>

.header{
    width: 300px;
    height: 95vh;
    border-right: 3px solid $nav-color;
    font-family: $NotoSans, serif;
    overflow-y: scroll;

    ul{
        margin-bottom: 30px;
    }

    ul p{
        border: none;
        padding: 0px;
        color: white;
        margin-bottom: 20px;
        text-transform: uppercase;
        font-weight: 800;
    }

    ul li{
        border-left: 1px solid $nav_text-color;
        padding: 15px;
        color: $nav_text-color;
        font-weight: 400;
    }

    ul li:hover{
        color: rgb(203 213 225);
        border-left: 2px solid rgb(203 213 225);
    }
}

a{
    all: unset;
    cursor: pointer;
}

</style>
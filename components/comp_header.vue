<template>
    <div class="header">
        <RouterLink to="/inazuma_eleven_1">Inazuma Eleven 1</RouterLink>
        <RouterLink to="/inazuma_eleven_2">Inazuma Eleven 2</RouterLink>
        <RouterLink to="/inazuma_eleven_3">Inazuma Eleven 3</RouterLink>
        <RouterLink to="/inazuma_eleven_go1">Inazuma Eleven Go 1</RouterLink>
        <RouterLink to="/inazuma_eleven_go2">Inazuma Eleven Go 2: Chrono Stones</RouterLink>
        <RouterLink to="/inazuma_eleven_go3">Inazuma Eleven Go 3: Galaxy</RouterLink>
    </div>
</template>

<script>

</script>

<style lang="scss" scoped>

.header{
    height: 95vh;
    border-right: 3px solid $nav-color;
    font-family: $NotoSans, serif;

    a{
        padding: 40px 30px;
        border-top: 2px solid white;
        text-align: center;
        color: white;
        width: 50%;
    }
}

.header a:last-child{
    border-bottom: 2px solid white;
}

a{
    all: unset;
    cursor: pointer;
}

</style>
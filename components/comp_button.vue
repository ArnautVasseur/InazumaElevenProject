<template>
    <button>
        <slot/>
    </button>
</template>

<script>

</script>

<style scoped lang="scss">

button{
    border: 1px solid white;
    color: white;
    background: none;
    padding: 10px 20px;
    cursor: pointer;
    transition: 0.15s ease-in-out;
}

button:hover{
    background: white;
    color: $primary-color;
    letter-spacing: 1px;
}

</style>
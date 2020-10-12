<template>
<div class="header">
    <ul class="navbar">
        <nuxt-link :to="{name: 'people'}" tag="li" class="navitem">People</nuxt-link>
        <li class="navitem">Transactions</li>
    </ul>
</div>
</template>

<script>
export default {

}
</script>

<style scoped>
.header {
    width: 100%;
    height: 60px;
    margin: 0;
    padding: 0;
    background-color: rgba(32, 178, 170, 1);
}

.header:hover {
    cursor: pointer;
}

ul.navbar {
    margin: 0;
    padding: 0;
    height: 100%;
    list-style-type: none;
    align-content: center;
    justify-content: flex-start;
}

.navitem {
    display: inline-block;
    align-content: center;
    height: 100%;
    padding: 18px 16px;
    color: white;
    font-weight: bold;
}

.navitem:hover {
    background-color: rgb(52, 198, 190)
}
</style>

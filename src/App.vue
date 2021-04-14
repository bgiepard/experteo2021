<template>
    <div class="flex-row">
        <header class="[ header ] flex-column justify-between align-center">
            <img src="./assets/pinlogo.png" alt="EkipyBudowlane" height="43">

            <ul class="flex-column" style="margin-top: 50px">
                <li><router-link to="/">Kategorie</router-link></li>
                <li><router-link to="/about">Artykuły</router-link></li>
            </ul>
        </header>
        <main class="[ main ] flex-row">
            <router-view/>
        </main>
    </div>
</template>

<style lang="less">
@import 'styles/reset.less';
@import 'styles/utilities.less';
@import 'styles/variables.less';

body {
    background: @bg-light;
    font-family: 'Baloo 2', sans-serif;
}

.header {
    padding: 20px;
}

.main {
    width: 100%;
}
</style>

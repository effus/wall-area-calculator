<template>
    <section class="section container">
        <div class="row">
            <div class="col s12 m10 offset-m1">
                <img alt="Vue logo" src="../assets/logo.png" class="project-logo z-depth-2">
                <h1 class="hide-on-small-only show-on-medium-and-up">Расчеты при ремонте квартиры</h1>
                <h4 class="hide-on-med-and-up show-on-small	">Расчеты при ремонте квартиры</h4>
                <div class="menu calc-menu">
                    <button class="btn-large  waves-effect waves-light" v-on:click="$emit('new-calc')">
                        <i class="material-icons left">add</i>
                        Площадь стен в комнате
                    </button>
                    <button class="btn-large  waves-effect waves-light" v-on:click="$emit('wp-calc')">
                        <i class="material-icons left">add</i>
                        Количество обоев
                    </button>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: 'HomeScreen'
}
</script>

<style lang="scss">
.project-logo {
    width: 20vw;
}
.calc-menu {
    display: flex;
    flex-direction: column;
}
</style>
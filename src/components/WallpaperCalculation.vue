<template>
    <section class="wp-calc section container">
        <a style="position:absolute; left: 2vw;" href="#back" v-on:click="$emit('back')">Назад</a>
        <h3>Расчет количества обоев</h3>
        <p>Для расчета необходимо произвести расчет площади стен</p>
        <div class="divider"></div>
        
        <div class="row">
            <h5 class="left">Параметры расчета</h5>
        </div>

        <form class="form">
            
            <div class="row">        
                <div class="input-field col s4">
                    <input type="number" class="validate" v-model="wallSpace">
                    <span class="helper-text" data-error="wrong" data-success="right">Площадь стен, м<span class="super">2</span></span>
                </div>

                <div class="input-field col s4">
                    <input type="number" class="validate" v-model="paperWidth">
                    <span class="helper-text" data-error="wrong" data-success="right">Ширина рулона обоев, см</span>
                </div>

                <div class="input-field col s4">
                    <input type="number" class="validate" v-model="paperLength">
                    <span class="helper-text" data-error="wrong" data-success="right">Длина рулона обоев, м</span>
                </div>
            </div>


            <div class="row">        
                <div class="col s10 m6">
                    <p class="result-line left">Количество рулонов:</p>
                    <p class="value">{{result}} шт.</p> 
                </div>
            </div>


        </form>
    </section>
</template>

<script>
export default {
    name: "WallpaperCalculation",
    data() {
        return {
            wallSpace: 0,
            paperWidth: 0,
            paperLength: 0
        }
    },
    computed: {
        result() {
            if (this.paperLength === 0 || this.paperWidth === 0) {
                return -1;
            }
            return Math.ceil(this.wallSpace / (this.paperWidth / 100 * this.paperLength));
        }
    }
}
</script>

<style lang="scss">
.wp-calc {
    .super {
        vertical-align: super;
        font-size: .7rem;
    }
    .result-line {
        font-size: 1.4rem;
        line-height: 150%;
    }
    .value {
        font-size: 1.4rem;
        line-height: 150%;
        color: rgb(136, 0, 0);
    }
}
</style>
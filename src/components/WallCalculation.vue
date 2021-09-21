<template>
    <section class="calculation section container">
        <a style="position:absolute; left: 2vw;" href="#back" v-on:click="$emit('back')">Назад</a>
        <h3>Расчет площади стен в комнате</h3>
        <p>Расчет производится с учетом прямоугольного помещения с ровными стенами и потолком.</p>
        <div class="divider"></div>
        
        <div class="row">
            <h5 class="left">Параметры помещения</h5>
        </div>

        <form class="form">
            
            <div class="row">        
                <div class="input-field col s8">
                    <input type="number" class="validate" v-model="l1">
                    <span class="helper-text" data-error="wrong" data-success="right">Длина стены #1, см</span>
                </div>
                <div class="col s4">
                    <img alt="wall 1" src="../assets/room-3d-l1.jpg" class="z-depth-1 hint-pic" />
                </div>
            </div>

            <div class="row">        
                <div class="input-field col s8">
                    <input type="number" class="validate" v-model="l2">
                    <span class="helper-text" data-error="wrong" data-success="right">Длина стены #2, см</span>
                </div>
                <div class="col s4">
                    <img alt="wall 1" src="../assets/room-3d-l2.jpg" class="z-depth-1 hint-pic" />
                </div>
            </div>

            <div class="row">        
                <div class="input-field col s8">
                    <input type="number" class="validate" v-model="h">
                    <span class="helper-text" data-error="wrong" data-success="right">Высота потолка, см</span>
                </div>
                <div class="col s4">
                    <img alt="wall 1" src="../assets/room-3d-h.jpg" class="z-depth-1 hint-pic" />
                </div>
            </div>

            <div class="divider"></div>

            <h5>Исключение площади стены</h5>
            <div class="row">        
                <div class="col s5">
                    <button type="button" class="btn-small waves-effect waves-light left" v-if="!flagExcludeForm" v-on:click="showExcludeForm">
                        <i class="material-icons left">add</i>
                        Добавить
                    </button>
                </div>
                <div class="col s3">
                    <ul class="collection" v-if="this.excludes.length > 0">
                        <li v-for="item in this.excludes" class="collection-item" v-bind:key="item.id">
                            <div>
                                {{item.w}} x {{item.h}} см2
                                <a href="javascript:" class="secondary-content" v-on:click="removeExclude(item)">
                                    <i class="material-icons">clear</i>
                                </a>
                            </div>
                        </li>
                    </ul>
                </div>
                <div class="col s4">
                    <img alt="wall 1" src="../assets/room-3d-exclude.jpg" class="z-depth-1 hint-pic" />
                </div>
            </div>

            <div class="row" v-if="flagExcludeForm">
                <div class="input-field col s3">
                    <input type="number" class="validate" v-model="excludedForm.w">
                    <span class="helper-text" data-error="wrong" data-success="right">Ширина, см</span>
                </div>
                <div class="input-field col s3">
                    <input type="number" class="validate" v-model="excludedForm.h">
                    <span class="helper-text" data-error="wrong" data-success="right">Высота, см</span>
                </div>
                <div class="col s3">
                    <button class="btn waves-effect waves-light" v-on:click="addExclude()">
                        <i class="material-icons left">add</i> Ок
                    </button>
                </div>
            </div>

            <div class="divider"></div>

            <div class="row">
                <div class="col s6">
                    <h4 class="left">Результат</h4>
                </div>
            </div>

            <div class="row">
                <div class="col s6">
                    <p class="result-line left">Площадь стен</p>
                </div>
                <div class="col s6">
                    <div class="result-line left">
                        <span class="value">{{result.walls}}</span> м<span class="super">2</span>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col s6">
                    <p class="result-line left">Площадь пола/потолка</p>
                </div>
                <div class="col s6">
                    <div class="result-line left">
                        <span class="value">{{result.floor}}</span> м<span class="super">2</span>
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col s6">
                    <p class="result-line left">Исключенная площадь</p>
                </div>
                <div class="col s6">
                    <div class="result-line left">
                        <span class="value">{{result.excluded}}</span> м<span class="super">2</span>
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col s6">
                    <p class="result-line left">Объем помещения</p>
                </div>
                <div class="col s6">
                    <div class="result-line left">
                        <span class="value">{{result.volume}}</span> м<span class="super">3</span>
                    </div>
                </div>
            </div>

        </form>
    </section>
</template>

<script>
export default {
    name: 'calculation',
    data() {
        return {
            l1: 0,
            l2: 0,
            h: 0,
            flagExcludeForm: false,
            excludes: [],
            result: {
                walls: .0,
                floor: 0,
                excluded: 0,
                volume: 0
            },
            excludedForm: {
                w: 0,
                h: 0
            }
        }
    },
    methods: {
        showError(e) {

        },
        showExcludeForm() {
            this.flagExcludeForm = true;
        },
        addExclude() {
            try {
                if (!parseFloat(this.excludedForm.w)) {
                    throw Error('Bad number');
                }
                if (!parseFloat(this.excludedForm.h)) {
                    throw Error('Bad number');
                }
                this.excludes.push({
                    id: Math.random().toString(),
                    w: parseFloat(this.excludedForm.w),
                    h: parseFloat(this.excludedForm.h)
                });
            } catch (e) {
                this.showError(e);
            }
            this.flagExcludeForm = false;
            this.excludedForm.w = 0;
            this.excludedForm.h = 0;
            this.makeCalculation();
        },
        removeExclude(removedItem) {
            this.excludes = this.excludes.filter(item => item.id != removedItem.id);
            this.makeCalculation();
        },
        makeCalculation() {
            this.result.floor = (this.l1 * this.l2) / 10000;
            this.result.volume = (this.l1 * this.l2 * this.h) / 1000000;
            const excludedAreas = this.excludes.map(item => {
                return item.w * item.h;
            });
            const excluded = excludedAreas.reduce((acc, s) => {
                return acc + s;
            }, 0);
            this.result.excluded = excluded / 10000;
            this.result.walls = ((this.l1 * this.h * 2) + (this.l2 * this.h * 2)) / 10000;
            if (this.result.excluded <= this.result.walls) {
                this.result.walls -= this.result.excluded;
            }
        }
    },
    watch: {
        l1() {
            this.makeCalculation();
        },
        l2() {
            this.makeCalculation();
        },
        h() {
            this.makeCalculation();
        }
    }
}
</script>

<style lang="scss">
.calculation {
    .result-line {
        font-size: 1.4rem;
        line-height: 150%;
        margin: 0;
        .value {
            color: rgb(136, 0, 0);
        }
        .super {
             vertical-align: super;
             font-size: 1.2rem;
        }
    }
    .hint-pic {
        height: 12vh;
    }
}
</style>
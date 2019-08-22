<template>
    <div class="calculator">
        <div class="display">{{ current || 0 }}</div>

        <div class="btn" @click="clear">C</div>
        <div class="btn" @click="sign">+/-</div>
        <div class="btn" @click="percent">%</div>
        <div class="btn operator" @click="divide">
            <i class="fas fa-divide fa-xs"></i>
        </div>

        <div class="btn" @click="append('7')">7</div>
        <div class="btn" @click="append('8')">8</div>
        <div class="btn" @click="append('9')">9</div>
        <div class="btn operator" @click="multiply">
            <i class="fas fa-times fa-xs"></i>
        </div>

        <div class="btn" @click="append('4')">4</div>
        <div class="btn" @click="append('5')">5</div>
        <div class="btn" @click="append('6')">6</div>
        <div class="btn operator" @click="subtract">
            <i class="fas fa-minus fa-xs"></i>
        </div>

        <div class="btn" @click="append('1')">1</div>
        <div class="btn" @click="append('2')">2</div>
        <div class="btn" @click="append('3')">3</div>
        <div class="btn operator" @click="add">
            <i class="fas fa-plus fa-xs"></i>
        </div>

        <div class="btn zero" @click="append('0')">0</div>
        <div class="btn" @click="dot">.</div>
        <div class="btn operator" @click="equal">
            <i class="fas fa-equals fa-xs"></i>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            previous: null,
            current: '',
            operator: null,
            operatorClicked: false
        }
    },

    methods: {
        clear() {
            this.current = ''
        },

        sign() {
            this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
        },

        percent() {
            this.current = `${parseFloat(this.current) / 100}`
        },

        append(number) {
            if (this.operatorClicked) {
                this.current = ''
                this.operatorClicked = false
            }

            this.current = `${this.current}${number}`
        },

        dot() {
            if (this.current.indexOf('.') === -1) {
                this.append('.')
            }
        },

        setPrevious() {
            this.previous = this.current
            this.operatorClicked = true
        },

        divide() {
            this.operator = (a, b) => a / b
            this.setPrevious()
        },

        multiply() {
            this.operator = (a, b) => a * b
            this.setPrevious()
        },

        subtract() {
            this.operator = (a, b) => a - b
            this.setPrevious()
        },

        add() {
            this.operator = (a, b) => a + b
            this.setPrevious()
        },

        equal() {
            this.current = `${this.operator(
                parseFloat(this.previous),
                parseFloat(this.current)
            )}`

            this.previous = null
        }
    }
}
</script>

<style scoped>
.calculator {
    margin: 0 auto;
    width: 350px;
    height: 300px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    font-size: 30px;
    user-select: none;
}

.display {
    grid-column: 1 / 5;
    background-color: #333;
    color: white;
    padding: 3%;
    overflow: hidden;
}

.btn {
    background-color: #f2f2f2;
    border: 1px solid gray;
    padding: 7%;
    cursor: pointer;
    transition: 0.4s;
}

.btn:active {
    background-color: white;
    transition: 0s;
}

.zero {
    grid-column: 1 / 3;
    padding: 4% !important;
}

.operator {
    background-color: orange;
    color: white;
}

.click-selected {
    background-color: gainsboro;
}

.fas {
    font-size: 1.2rem;
}
</style>

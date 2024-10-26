<template>
    <h1>Calculadora</h1>
    <div class="calculadora">
        <div class="display">{{ valorCorrente || '0' }}</div>
        <div v-on:click="limpar" class="botao">C</div>
        <div v-on:click="sinal" class="botao">+/-</div>
        <div v-on:click="porcentagem" class="botao">%</div>
        <div v-on:click="dividir" class="botaoOperadores">÷</div>
        <div v-on:click="juntarNumeros('7')" class="botao">7</div>
        <div v-on:click="juntarNumeros('8')" class="botao">8</div>
        <div v-on:click="juntarNumeros('9')" class="botao">9</div>
        <div v-on:click="multiplicar" class="botaoOperadores">x</div>
        <div v-on:click="juntarNumeros('4')" class="botao">4</div>
        <div v-on:click="juntarNumeros('5')" class="botao">5</div>
        <div v-on:click="juntarNumeros('6')" class="botao">6</div>
        <div v-on:click="diminuir" class="botaoOperadores">-</div>
        <div v-on:click="juntarNumeros('1')" class="botao">1</div>
        <div v-on:click="juntarNumeros('2')" class="botao">2</div>
        <div v-on:click="juntarNumeros('3')" class="botao">3</div>
        <div v-on:click="somar" class="botaoOperadores">+</div>
        <div v-on:click="juntarNumeros('0')" class="botao zero">0</div>
        <div v-on:click="ponto" class="botao">.</div>
        <div v-on:click="resultado" class="botaoOperadores">=</div>

        <!-- Novas funcionalidades -->
        <div v-on:click="logaritmoBase10" class="botaoNovasOperadores">log10</div>
        <div v-on:click="logaritmoBase" class="botaoNovasOperadores">log(a)b</div>
        <div v-on:click="raizQuadrada" class="botaoNovasOperadores">Sqrt</div>
        <div v-on:click="raiz" class="botaoNovasOperadores ">Pow(1/n)</div>
        <div v-on:click="aoQuadrado" class="botaoNovasOperadores">Pow(2)</div>
        <div v-on:click="potencia" class="botaoNovasOperadores">Pow(n)</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            valorCorrente: '',
            numeroAnterior: null,
            operador: null,
            operadorClicado: false,
        };
    },
    methods: {
        limpar() {
            this.valorCorrente = '';
            this.numeroAnterior = null;
            this.operador = null;
            this.operadorClicado = false;
        },
        sinal() {
            this.valorCorrente = this.valorCorrente.charAt(0) === '-'
                ? this.valorCorrente.slice(1)
                : `-${this.valorCorrente}`;
        },
        porcentagem() {
            if (this.valorCorrente) {
                this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
            }
        },
        juntarNumeros(numero) {
            if (this.operadorClicado) {
                this.valorCorrente = '';
                this.operadorClicado = false;
            }
            this.valorCorrente = `${this.valorCorrente}${numero}`;
        },
        ponto() {
            if (this.valorCorrente.indexOf('.') === -1) {
                this.juntarNumeros('.');
            }
        },
        setarValor() {
            this.numeroAnterior = this.valorCorrente;
            this.operadorClicado = true;
        },
        dividir() {
            if (this.valorCorrente) {
                this.operador = (num1, num2) => {
                    if (num2 === 0) {
                        alert('Erro: Divisão por zero');
                        return '0';
                    }
                    return num1 / num2;
                };
                this.setarValor();
            }
        },
        multiplicar() {
            this.operador = (num1, num2) => num1 * num2;
            this.setarValor();
        },
        diminuir() {
            this.operador = (num1, num2) => num1 - num2;
            this.setarValor();
        },
        somar() {
            this.operador = (num1, num2) => num1 + num2;
            this.setarValor();
        },
        resultado() {
            if (this.numeroAnterior && this.valorCorrente) {
                this.valorCorrente = `${this.operador(
                    parseFloat(this.numeroAnterior),
                    parseFloat(this.valorCorrente),
                )}`;
                this.numeroAnterior = null;
            }
        },
        logaritmoBase10() {
            if (this.valorCorrente) {
                this.valorCorrente = `${Math.log10(parseFloat(this.valorCorrente))}`;
            }
        },
        logaritmoBase() {
            const base = parseFloat(prompt("Informe a base:"));
            if (this.valorCorrente && base > 0 && base !== 1) {
                this.valorCorrente = `${Math.log(parseFloat(this.valorCorrente)) / Math.log(base)}`;
            } else {
                alert("Base inválida. A base deve ser maior que 0 e diferente de 1.");
            }
        },
        raizQuadrada() {
            if (this.valorCorrente) {
                this.valorCorrente = `${Math.sqrt(parseFloat(this.valorCorrente))}`;
            }
        },
        raiz() {
            const base = parseFloat(prompt("Informe o valor da raiz:"));
            if (this.valorCorrente && base > 0) {
                this.valorCorrente = `${Math.pow(parseFloat(this.valorCorrente), 1 / base)}`;
            } else {
                alert("Valor inválido para a raiz. Deve ser maior que 0.");
            }
        },
        aoQuadrado() {
            if (this.valorCorrente) {
                this.valorCorrente = `${Math.pow(parseFloat(this.valorCorrente), 2)}`;
            }
        },
        potencia() {
            const expoente = parseFloat(prompt("Informe o expoente:"));
            if (this.valorCorrente) {
                this.valorCorrente = `${Math.pow(parseFloat(this.valorCorrente), expoente)}`;
            }
        },
    },
};
</script>

<style scoped>
.calculadora {
    margin: 0 auto;
    width: 350px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    cursor: pointer;
}
h1 {
    padding-bottom: 10px;
    font-size: 2em;
}
.display {
    grid-column: 1 / 5;
    background-color: #333;
    color: white;
}
.zero {
    grid-column: 1 / 3;
}
.botao {
    background-color: #f2f2f2;
    border: 1px solid #999;
}
.botaoOperadores {
    background-color: orange;
    color: white;
    border: 1px solid #999;
}

.botaoNovasOperadores {
    background-color: orange;
    color: white;
    border: 1px solid #999;
}
</style>

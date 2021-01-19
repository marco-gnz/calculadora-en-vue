<template>
  <div class="container-fluid calculadora">
    <div class="row">
      <h1 class="title">Calculadora básica :)</h1>
      <div class="calculadora-dos">
        <!-- barra de resultado -->
        <div class="resultado">{{ number || "0" }}</div>
        <!-- Nº y operadores -->
        <div class="calculadora-tres">
          <div @click="clear" class="btn clear"><b>C</b></div>
          <div @click="remove" class="btn remove">Borr</div>
          <div @click="sign" class="btn operador">+/-</div>
          <div @click="porcentaje" class="btn operador">%</div>
          <div @click="append('7')" class="btn">7</div>
          <div @click="append('8')" class="btn">8</div>
          <div @click="append('9')" class="btn">9</div>
          <div @click="multiplicacion" class="btn operador">x</div>
          <div @click="append('4')" class="btn">4</div>
          <div @click="append('5')" class="btn">5</div>
          <div @click="append('6')" class="btn">6</div>
          <div @click="resta" class="btn operador">-</div>
          <div @click="append('1')" class="btn">1</div>
          <div @click="append('2')" class="btn">2</div>
          <div @click="append('3')" class="btn">3</div>
          <div @click="suma" class="btn operador">+</div>
          <div @click="append('0')" class="btn">0</div>
          <div @click="punto" class="btn">.</div>
          <div @click="divicion" class="btn operador">/</div>
          <button
            type="button"
            @click.prevent="equal"
            @keyup.enter="equal"
            class="btn operador"
          >
            =
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculadora",
  data() {
    return {
      prevNum: null,
      number: "",
      operador: null,
      operadorClicked: false,
    };
  },
  methods: {
    clear() {
      //metodo para borrar números en la barra de resultados
      this.number = "";
    },
    sign() {
      //metodo para aplicar signo + o -
      //propiedad chartAt proporciona un entero (0 y 1).Si no tiene nada, utilizará 0.
      this.number =
        this.number.charAt(0) === "-"
        // metodo slice es para que comience desde el primer carcater (1).
          ? this.number.slice(1)
          : `-${this.number}`;
    },
    porcentaje() {
      //metodo para calcular porcentaje del numero ingresado al presional el boton %. 
      // funcion parseFloat es para convertir la cadena de carcateres a un numero.
      this.number = `${parseFloat(this.number) / 100}`;
    },
    append(num) {
      //metodo recibe el numero clickeado, que al prinicipio esta en false.
      //meotodo para juntar los numeros clickeados
      if (this.operadorClicked) {
        (this.number = ""), (this.operadorClicked = false);
      }
      this.number = `${this.number}${num}`;
    },
    punto() {
      //metodo para indexar el punto. 
      //si el indice en este caso es mayor o igual a la longitud del nº, devuelve -1, por lo que lo adjuntara al n clickeado. append()
      if (this.number.indexOf(".") === -1) {
        this.append(".");
      }
    },
    remove() {
      //meotodo para borrar los nº ingresados, el slice comienza del 0 o del -1, osea borrará desde el ultimo nº ingresado.
      this.number = this.number.slice(0, -1);
    },
    setPrevNum() {
      //metodo para el primer n pase al n ingresado. Por lo que al presionar el div sera un valor true.
      this.prevNum = this.number;
      this.operadorClicked = true;
    },
    suma() {
      //metodo para sumar, donde recibe dos caractetes, (a,b) prevNum. y los suma
      this.operador = (a, b) => a + b;
      this.setPrevNum();
    },
    resta() {
      //metodo para restar, donde recibe dos caractetes, (a,b) prevNum. y los resta
      this.operador = (a, b) => a - b;
      this.setPrevNum();
    },
    multiplicacion() {
      //metodo para multiplicar, donde recibe dos caractetes, (a,b) prevNum. y los multiplica
      this.operador = (a, b) => a * b;
      this.setPrevNum();
    },
    divicion() {
      //metodo para dividir, donde recibe dos caractetes, (a,b) prevNum. y los divide
      this.operador = (a, b) => a / b;
      this.setPrevNum();
    },
    equal() {
      //metodo para calcular operador, donde se parsean los dos numeros para convertirlo en un solo numero.
      this.number = `${this.operador(
        parseFloat(this.prevNum),
        parseFloat(this.number)
      )}`;
      this.prevNum = null;
    },
  },
};
</script>

<style>
.calculadora-dos {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  width: 400px;
  font-size: 30px;
}
.resultado {
  grid-column: 1/5;
  background-color: rgba(0, 150, 82, 0.678) !important;
  color: #fff;
  border-radius: 30px 30px 30px 30px;
}
.calculadora-tres {
  padding-top: 20px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  width: 400px;
  font-size: 30px;
}
.clear {
  grid-column: 1/2;
}
.remove {
  grid-column: 3/2;
  background-color: rgb(65, 184, 131, 0.9) !important;
  color: #fff;
}
.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
  border-radius: 60px 60px 60px 60px;
  margin-top: 10px;
  margin-left: 6px;
}
.operador {
  background-color: rgb(53, 73, 94);
  color: #fff;
}
</style>
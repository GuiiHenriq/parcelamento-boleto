<template>
  <div>
    <form>
      <h1>Digite o valor:</h1>
      <input name="busca" id="busca" type="text" v-model="busca" placeholder="R$ 2599">
      <input type="submit" id="lupa" value="Buscar" @click.prevent="parcelamento(0.0299, 0.0349)">
      <p>inserir valor sem cifrão e pontos</p>
    </form>
    <section v-if="listValorParcelado.length">
      <ul class="grupos">
        <li @click="parcelamento(0.0299, 0.0349)"><h1>PicPay</h1></li>
        <li @click="parcelamento(0, 0.0400)"><h1>Mercado Crédito</h1></li>
        <li @click="parcelamento(0, 0.0500)"><h1>Virtus Pay</h1></li>
        <li @click="parcelamento(0, 0.0160)"><h1>Emprestimo Sim</h1></li>
      </ul>
      <ul class="valores">
        <li v-for="(valor, index) in listValorParcelado" :key="index">
          <p>{{valor}}</p> <span>Total de</span> <p>R$</p> <p>{{listValorTotal[index]}}</p>
        </li>
      </ul>
    </section>
    <footer>
      <p>As taxas foram retiradas do próprio site de cada empresa.</p>
      <p>Podendo serem alteradas sem aviso prévio!</p>
      <a href="https://www.picpay.com/" target="_blank">www.picpay.com</a>
      <a href="https://www.mercadolivre.com.br/ajuda/Como-comprar-com-Mercado-Cr-di_3947" target="_blank">www.mercadolivre.com.br</a>
      <a href="https://www.usevirtus.com.br/" target="_blank">www.usevirtus.com.br</a>
      <a href="https://emprestimosim.com.br/" target="_blank">www.emprestimosim.com.br</a>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'Parcelado',
  data() {
    return {
      busca: '',
      ativo: false,
      valorParcelado: '',
      valorTotal: '',
      listValorParcelado: [],
      listValorTotal: []
    };
  },
  methods: {
    parcelamento(jurosBoleto, jurosParcela) {
      let parcela;
      let valorInt = parseFloat(this.busca);

      this.listValorParcelado = [];
      this.listValorTotal = [];
      this.ativo = false;
      
      if (this.busca == null || this.busca == 0 || this.busca == " " || this.busca == isNaN) {
        alert('Digite o valor corretamente');
        return 0;
      }

      valorInt += valorInt * jurosBoleto;
      this.valorParcelado = valorInt;
      this.valorTotal = valorInt;
      

      for (parcela = 1; parcela <= 12; parcela++) {
        if (parcela == 1) {
          this.valorParcelado;
          this.valorTotal;
        } else {
          this.valorParcelado = valorInt * jurosParcela / (1 - Math.pow(1 + jurosParcela, -parcela));
          this.valorTotal = this.valorParcelado * parcela;
        }

        this.listValorParcelado.push(parcela + "x \t" + "R$ " + parseFloat(this.valorParcelado).toFixed(2));
        this.listValorTotal.push(parseFloat(this.valorTotal).toFixed(2));
      }

      this.ativo = true;
    }
  },
  computed: {
    calc() {
      return this.listValorParcelado.map((valor, i) => {
        return {
          valor: valor,
          listValorTotal: this.valorTotal[i]
        }
      })
    }
  }
}
</script>

<style scoped>
form {
  max-width: 600px;
  margin: 30px auto 20px auto;
  position: relative;
}

form h1 {
  margin-bottom: 0.5rem;
}

#busca {
  width: 100%;
  padding: 20px;
  border: none;
}

#busca:focus,
#busca:hover {
  transform: scale(1.1);
}

#lupa {
  width: 62px;
  height: 62px;
  background: url("../assets/search.svg") no-repeat center center;
  text-indent: -150px;
  border: none;
  cursor: pointer;
  position: absolute;
  right: 0px;
  box-shadow: none;
}

.grupos {
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  max-width: 600px;
  margin: 0 auto;
  position: relative;
}

.grupos li h1 {
  font-size: 1.25rem;
}

.grupos li {
  display: inline-block;
  padding: 0 1rem;
  cursor: pointer;
}

.grupos li:hover {
  background: gray;
  color: white;
  border-radius: 4px;
}

.grupos li.active {
  background: gray;
  color: white;
  border-radius: 4px;
}

.valores {
  max-width: 600px;
  margin: 0 auto;
  position: relative;
}

.valores li {
  border: 1px solid #95a5a6;
  border-radius: 4px;
  padding: 12px;
  margin-top: 10px;
  font-size: 1.2rem;
}

.valores li p {
  display: inline-block;
  font-weight: bold;
}

.valores li span {
  font-size: 1.35rem;
}

footer {
  max-width: 600px;
  background: white;
  margin: 40px auto 60px auto;
  position: relative;
}

footer p {
  text-align: center;
  margin: 0;
  font-size: 1.2rem;
}

footer a {
  display: block;
  text-align: center;
  text-decoration: underline;
}
</style>

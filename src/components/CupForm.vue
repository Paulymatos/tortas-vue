<template>
  <div>
   <Message :msg="msg" v-show="msg"/>
  </div>
  <form id="cup-form" @submit="createCake">
    <div class="input-container">
      <label for="nome">Nome do Cliente</label>
      <input
        type="text"
        id="nome"
        name="name"
        v-model="nome"
        placeholder="Digite o seu nome"
      />
    </div>
    <div class="input-container">
      <label for="massa">Escolha a massa</label>
      <select name="massa" id="massa" v-model="massa">
        <option value="">Selecione sua massa</option>
        <option v-for="massa in massas" :key="massa.id" :value="massa.tipo">
          {{ massa.tipo }}
        </option>
      </select>
    </div>
    <div class="input-container">
      <label for="recheio">Escolha o recheio</label>
      <select name="recheio" id="recheio" v-model="recheio">
        <option value="">Selecione seu recheio</option>
        <option
          v-for="recheio in recheios"
          :key="recheio.id"
          :value="recheio.tipo"
        >
          {{ recheio.tipo }}
        </option>
      </select>
    </div>
    <div class="input-container">
      <label for="cobertura">Escolha a cobertura</label>
      <select name="cobertura" id="cobertura" v-model="cobertura">
        <option value="">Selecione sua cobertura</option>
        <option
          v-for="cobertura in coberturas"
          :key="cobertura.id"
          :value="cobertura.tipo"
        >
          {{ cobertura.tipo }}
        </option>
      </select>
    </div>
    <div id="opcionais-container" class="input-container">
      <label id="opcionais-titulo" for="Opcionais"
        >Selecione os opcionais:</label
      >
      <div
        class="checkbox-container"
        v-for="opcional in opcionaisdata"
        :key="opcional.id"
      >
        <input
          type="checkbox"
          name="opcionais"
          v-model="opcionais"
          :value="opcional.tipo"
        />
        <span>{{ opcional.tipo }}</span>
      </div>
    </div>
    <div class="input-container">
      <input type="submit" class="submit-btn" value="Montar meu Cupcake" />
    </div>
  </form>
</template>
<script>
import Message from './Message.vue'

export default {
  name: "CupForm",
  data() {
    return {
      massas: null,
      recheios: null,
      coberturas: null,
      opcionaisdata: null,
      nomecliente: null,
      massa: null,
      recheio: null,
      cobertura: null,
      opcionais: [],
      status: "solicitado",
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();
      this.massas = data.massas;
      this.coberturas = data.coberturas;
      this.recheios = data.recheios;
      this.opcionaisdata = data.opcionais;
    },
    async createCake(e){
    e.preventDefault()
    
    const data = {
      nome: this.nome,
      massa:this.massa,
      cobertura:this.cobertura,
      recheio:this.recheio,
      opicionais: Array.from(this.opcionais),
      status:"Solicitado"

    }
    const dataJson= JSON.stringify(data)
    const req= await fetch("http://localhost:3000/tortas",{
      method:"POST",
      headers:{"Content-type":"application/json"},
      body:dataJson
    
    })
   
    const res = await  req.json()
    // colocar uma msg de sistema
     this.msg= `Pedido n°${res.id} realizado com Sucesso`
      // limpar msg
     setTimeout(() => this.msg="",3000)
    // limpar os campos
      this.nome =""
      this.massa = ""
      this.cobertura= ""
      this.recheio = ""
      this.opcionais = ""

  },
  },
   mounted() {
    this.getIngredientes();
  },
  components:{
    Message
  }
 
};
</script>
<style scoped>
#cup-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #a2d2ff;
  padding: 5px 10px;
  border-left: 4px solid #ffafcc;
}
input,
select {
  padding: 5px 10px;
  width: 300px;
}

#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#opcionais-titulo {
  width: 100%;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
  color: rgb(187, 183, 183);
}
.submit-btn {
  background-color: #fcd5ce;
  color: #ff006e;
  border-radius: 20px;
  border: none;
  font-weight: bold;
  padding: 10px;
  font-size: 15px;
  margin-bottom: 15px;
  cursor: pointer;
  width: 200px;
  transition: 0.5s;
}
</style>
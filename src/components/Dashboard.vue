<template>
  <div id="cake-table">
    <div>
      <div id="cake-table-heading">
        <div class="order-id">1</div>
        <div>Cliente:</div>
        <div>Massa</div>
        <div>Recheio</div>
        <div>Cobertura</div>
        <div>Opcionais</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="cake-table-rows">
      <div class="cake-table-row" v-for="pedido in pedidos" :key="pedido.id">
        <div class="order-number">{{ pedido.id }}</div>
        <div>{{ pedido.nome }}</div>
        <div>{{ pedido.massa }}</div>
        <div>{{ pedido.recheio }}</div>
        <div>{{ pedido.cobertura }}</div>
        <div>
          <ul v-for="(opcional, index) in pedido.opcionais" :key="index">
            <li>{{opcional}}</li>
          </ul>          
        </div>
        <div class="botoes">
          <select name=" Status" class="status">
            <option value="">Selecione</option>
            <option  v-for="s in status" :key="s.id" :value="s.tipo" :selected="pedido.status == s.tipo">
                 {{s.tipo}}
            </option>
           
          </select>
          <button class="delete-btn" @click="deleteCake(pedido.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dashboard",
  data() {
    return {
      pedidos: null,
      pedidos_id: null,
      status: [],
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/tortas");

      const data = await req.json();
      this.pedidos = data;
      console.log('->>>', this.pedidos)
      // resgatar os status dos pedidos
      this.getStatus()
    },
    async getStatus(){
        const req = await fetch('http://localhost:3000/status')
        const data= await req.json()
        this.status= data
     
    },
    // Deletar pedidos
    async deleteCake(id){
      const req= await fetch(`http://localhost:3000/tortas/${id}`,{
        method:"DELETE"
     })
     const res= await req.json()
     //msg
     this.getPedidos()
    }
  },
  mounted() {
    this.getPedidos();
  },
};
</script>
<style scoped>
#cake-table {
  max-width: 1200px;
  margin: 0 auto;
}

#cake-table-heading,
#cake-table-rows,
.cake-table-row {
  display: flex;
  flex-wrap: wrap;
}

#cake-table-heading {
  font-weight: bold;
  padding: 10px;
  border-bottom: 1px solid rgb(226, 225, 225);
}

.cake-table-row {
  width: 100%;
  padding: 10px;
  border-bottom: 1px solid rgb(226, 225, 225);
}

#cake-table-heading div,
.cake-table-row div {
  width: 15%;
}

#cake-table-heading .order-id,
.cake-table-row .order-number {
  width: 5%;
}
.botoes{
    display: flex;
}

select {
  padding: 10px;
  margin-right: 12px;
  background-color: #ffc4d6;
  color: white;
  font-weight: bold;
  font-size: 13px;
  border: none;
  border-radius: 10px;
  width: 103px;
  height: 45px;
}

.delete-btn {
  background-color: #ffc4d6;
  color: white;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 13px;
  cursor: pointer;
  transition: 0.5s;
  border: none;
  border-radius: 10px;
  width: 100px;
  height: 45px;
}

.delete-btn:hover {
  background-color: transparent;
  color: #a2d2ff;
}
option{
  background-color:#a2d2ff;
}
</style>
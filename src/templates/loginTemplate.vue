<template>
  <span>
    <header>
      <navbar cor="teal darken-2" url="/" logo="Social">
          <li v-if="usuario"><router-link to="/">Home</router-link></li>
          <li v-if="!usuario"><router-link to="/login">Entrar</router-link></li>
          <li v-if="!usuario"><router-link to="/cadastro">Cadastre-se</router-link></li>
          <li v-if="usuario"><router-link to="/perfil">{{usuario.name}}</router-link></li>
          <li v-if="usuario"><a v-on:click="sair()" to="/login">Sair</a></li>
      </navbar>
    </header>
    <main>
      <div class="container">
        <div class="row">
          <!-- <grade tamanho="8">
              <slot name="menuesquerdo"/>
              <cartaomenu>
                <h4>SPA utilizando Vue.js e Laravel.</h4>
              </cartaomenu> 
              
          </grade> -->
          <grade tamanho="4">
           <slot name="principal"/>
          </grade>
        </div>
      </div>
    </main>
    <!-- <rodape cor="teal darken-2" logo="Social" descricao="Teste de descricao" ano="2021">
      <li><a class="grey-text text-lighten-3" href="#!">Home</a></li>
      <li><a class="grey-text text-lighten-3" href="#!">Link 2</a></li>
      <li><a class="grey-text text-lighten-3" href="#!">Link 3</a></li>
      <li><a class="grey-text text-lighten-3" href="#!">Link 4</a></li>
    </rodape> -->
  </span>
</template>

<script>
import navbar from "@/components/layout/navbar";
import rodape from "@/components/layout/rodape";
import grade from "@/components/layout/grade";
import cartaomenu from "@/components/layout/cartaomenu";
import cartaoConteudo from "@/components/social/cartaoConteudo";


export default {
  name: "loginTemplate",
  data(){
    return {
      usuario:false
    }
  },
  components: {
    navbar,
    rodape,
    grade,
    cartaomenu,
    cartaoConteudo
  },
  created(){
    let usuarioAux = this.$store.getters.getUsuario;
    if (usuarioAux){
      this.usuario = this.$store.getters.getUsuario;
      this.$router.push('/');
    }
  },
  methods:{
   
  }

};
</script>

<style>
h4{
  color:rgb(5, 4, 4);
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
cartaomenu{
  text-align: center;
}
body{
  background-color: rgb(255, 255, 255);
}
</style>

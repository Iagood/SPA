<template>
  <div class="row">
    <div class="card">
      <div class="card-content">
        <div class="row valign-wrapper">
          <grade tamanho="1">
            <img :src="perfil" :alt="nome" class="circle responsive-img" />
            <!-- notice the "circle" class -->
          </grade>
          <grade tamanho="11">
            <span class="black-text">
              <strong>{{ nome }}</strong> - <small>{{ data }} 11:37</small>
            </span>
          </grade>
        </div>

        <slot />
      </div>
      <div class="card-action">
        <p>
          <a style="cursor:pointer" @click="curtida(id)"> <i class="material-icons">{{ curtiu }}</i> {{ totalCurtidas }}</a>
          <i class="material-icons">insert_comment</i>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import grade from "@/components/layout/grade";
export default {
  name: "CardConteudo",
  props: ["id", "perfil", "nome", "data"],
  data() {
    return {
      curtiu: "favorite_border",
      totalCurtidas: 0,
    };
  },
  components: {
    grade,
  },
  methods: {
    curtida(id) {
      this.$http
        .put(
          this.$urlAPI + `conteudo/curtir/` + id,
          {},
          {
            headers: {
              authorization: "Bearer " + this.$store.getters.getToken,
            },
          }
        )
        .then((response) => {
          if (response.status) {
            this.totalCurtidas = response.data.curtidas;
            if (this.curtiu == "favorite_border") {
              this.curtiu = "favorite";
            } else {
              this.curtiu = "favorite_border";
            }
          } else {
            alert(response.data.erro);
          }
        })
        .catch((e) => {
          console.log(e);
          alert("Erro! Tente novamente mais tarde!");
        });
    },
  },
};
</script>

<!-- Estilo da página -->
<style scoped>
</style>
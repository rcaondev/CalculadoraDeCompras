<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Calculadora de Compras</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <div class="container">
        <ion-item>
          <ion-label position="floating">Nome do Produto</ion-label>
          <ion-input v-model="nomeProduto" type="text"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label position="floating">Preço (R$)</ion-label>
          <ion-input v-model="precoProduto" type="number"></ion-input>
        </ion-item>

        <ion-button expand="full" @click="adicionarProduto">Adicionar Produto</ion-button>

        <ion-list>
          <ion-item v-for="(produto, index) in carrinho" :key="index">
            <ion-label>{{ produto.nome }} - R$ {{ produto.preco.toFixed(2) }}</ion-label>
            <ion-button @click="removerProduto(index)" color="danger">Remover</ion-button>
          </ion-item>
        </ion-list>

        <ion-item>
          <ion-label>Total: R$ {{ total.toFixed(2) }}</ion-label>
        </ion-item>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonItem,
  IonLabel,
  IonInput,
  IonButton,
  IonList,
} from '@ionic/vue';

export default {
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonItem,
    IonLabel,
    IonInput,
    IonButton,
    IonList,
  },
  data() {
    return {
      nomeProduto: '',
      precoProduto: 0,
      carrinho: [],
    };
  },
  computed: {
    total() {
      return this.carrinho.reduce((acc, produto) => acc + produto.preco, 0);
    },
  },
  methods: {
    adicionarProduto() {
      if (this.nomeProduto && this.precoProduto > 0) {
        this.carrinho.push({
          nome: this.nomeProduto,
          preco: parseFloat(this.precoProduto),
        });
        this.nomeProduto = '';
        this.precoProduto = 0;
      }
    },
    removerProduto(index) {
      this.carrinho.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.container {
  padding: 20px;
}
</style>
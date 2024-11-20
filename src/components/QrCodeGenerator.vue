<template>
  <div class="wrapper">
    <div class="all">
      <div class="header-form">
        <h1>Gerador de QRCode</h1>
        <p>Cole a URL desejada:</p>
      </div>

      <!-- Formulário -->
      <div class="form">
        <input
          v-model="inputValue"
          type="text"
          placeholder="Insira a URL"
          name="url"
          id="url"
          @keyup="resetQRCode"
        />
        <button @click="generateQRCode" id="btn">
          {{ isLoading ? "Gerando QRCode..." : "Gerar QRCode" }}
        </button>
      </div>
    </div>

    <!-- QR Code gerado -->
    <div class="image" v-if="qrCodeUrl">
      <img :src="qrCodeUrl" id="imgQrCode" alt="QR Code Gerado" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "", // Valor do campo de entrada
      qrCodeUrl: "", // URL do QR Code gerado
      isLoading: false, // Controle de carregamento
    };
  },
  methods: {
    generateQRCode() {
      if (!this.inputValue) {
        alert("Nenhuma URL encontrada"); // Alerta caso o campo esteja vazio
        return;
      }

      this.isLoading = true; // Define o estado como carregando
      this.qrCodeUrl = `https://api.qrserver.com/v1/create-qr-code/?size=170x170&data=${encodeURIComponent(
        this.inputValue
      )}`; // Gera o QR Code

      // Simula o carregamento da imagem
      const img = new Image();
      img.src = this.qrCodeUrl;
      img.onload = () => {
        this.isLoading = false; // Finaliza o carregamento
        document.querySelector(".wrapper").classList.add("active"); // Adiciona a classe ativa
      };
    },
    resetQRCode() {
      if (!this.inputValue) {
        document.querySelector(".wrapper").classList.remove("active"); // Remove a classe ativa se o campo estiver vazio
      }
    },
  },
};
</script>

<style scoped>

.wrapper {
  background-color: #ffffff;
  padding-right: 50px;
  margin-top: 40px;
  height: 350px;
  width: 600px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.wrapper.active {
  height: 300px;
}

.wrapper h1 {
font-size: 1.7rem
}

.all{
  padding-left: 50px;
  margin-right: 10px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items:    center;
}

.header-form p {
  font-size: 1.1rem;
  margin-block: 5px;
}

.form {
  align-items: center;
  justify-content: center;
  flex-direction: column-reverse;
  padding: 10px;
  font-size: 16px;
  width: 100%;
  align-items: center;
  margin-bottom: 10px;
  margin-top: 15px;
}

.form:hover {
  cursor: pointer;
}

.wrapper .form input {
  background-color: transparent;
  width: 100%;
  outline: none;
  height: 40px;
  margin-bottom: 2rem;
  border: none;
  border-bottom: .1rem solid #0056b3;
}

.wrapper .form input::placeholder {
  color: #4f4e4e;
  font-size: 14px;
}

.image {
  padding-right: 30px;
}

#btn {
  width:100%;
  height: 35px;
  background-color: #1a6abf;
  outline: none;
  border: none;
  border-radius: 5px;
  color: #eee;
  cursor: pointer;
}

.wrapper .image {
  display: none;
  padding: 10px;
  margin-top: 20px;
  margin-left: 20px;
  margin-right: 10px;
  border-radius: 5px;
  pointer-events: none;
  border: 1px solid #ccc
}

.wrapper .image img {
  width: 170px;
}

.wrapper.active .image {
  display: block;
  transition: all .5s .5s ease;
}
</style>
<template>
  <div>
    <NavegacaoComponente></NavegacaoComponente>
    <div style="background: #AF3437
;">
      <div style="display: flex; flex-direction: row; max-width: 1260px; margin: 0 auto; justify-content: space-between;">
        <div>
          <div style="display: flex; justify-content: left; margin-top: 50px; margin-bottom: 40px;">
            <img src="./assets/letreiro.svg" class="imagem-cipa" style="width: 200px">
          </div>
          <div style="font-weight: 400;">
            <p class="paragrafo">
              <strong style="color: #fff; font-size: 24px;">O Gerador DANFe da LEFISC é uma ferramenta simples que transforma uma NFe de modelo 55 (em .xml ou .zip) em um DANFE, pronto para você imprimir, sem burocracias.</strong>
              <br><br>
              O DANFE é utilizado para acompanhar o trânsito da mercadoria. É uma representação gráfica simplificada da Nota Fiscal Eletrônica, em papel comum e em via única.
            </p>
          </div>
        </div>
        <div>
          <img src="./assets/slaoqehisso.svg" class="imagem-person">
        </div>
      </div>
    </div>

    <div style="padding-bottom: 40px; background: #EA4753;">
      <div class="search-bar" >
        <EnviarComponente></EnviarComponente>
       
          

  </div>
</div>


    <FutterComponente></FutterComponente>
  </div>
</template>

<script>

import NavegacaoComponente from './components/NavegacaoComponente.vue';
import FutterComponente from './components/FutterComponente.vue';
import EnviarComponente from './components/EnviarComponente.vue';

export default {
  components: {
    NavegacaoComponente,
    FutterComponente,
    EnviarComponente,
  }}


</script>

<style>




* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
  outline: none;
}
.imagem-cipa {
  max-width: 100%;
  height: auto;
}

.imagem-person {
  width: 100%;
  max-width: 600px;
  height: auto;
  margin-top: 100px;
}

.paragrafo {
  width: 550px;
  margin: 0 auto;
  font-size: 24px;
  margin-bottom: 80px;
  text-align: justify;
  color: white;
  
}

.search-bar {
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
  background: #fff;
  top: -36px;
  border-radius: 5px;
  padding: 10px 30px;
}

.search-select,
.search-input {
  font-size: 16px;
  height: 40px;
  border: none;
  border-radius: 6px;
  padding: 0px 10px;
}

.search-select {
  width: 300px; 
  height: 40px;
  padding: 10px;
}

.search-label {
  color: white;
  margin-right: 12px;
  font-weight: 500;
}

.search-input {
  width: 100%;
  max-width: 290px;
  
  font-weight: 600;
}


</style>
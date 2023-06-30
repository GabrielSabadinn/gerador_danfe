<template>
  <div>
    <div class="atePassoDois" >
        <label for="assetsFieldHandle" style="display: flex; align-items: center; justify-content: center; background: #AF3437; cursor: pointer; width: 100%; height: 40px; border-radius:10px; margin: 20px 0px 10px;"><p style="font-size: 16px; margin: 0px; color: rgb(255, 255, 255);font-weight:600;"> <img src="../assets/dowload.svg" style="margin-right: 6px;">Clique aqui para selecionar os arquivos .XML ou .ZIP</p></label>
        <input type="file" multiple name="fields[assetsFieldHandle][]" id="assetsFieldHandle" style="display: none;" class="w-px h-px opacity-0 overflow-hidden absolute" @change="onChange" ref="file" accept=".zip,.xml" />
        <div class="flex w-full h-screen items-center justify-center text-center">
       
        
        <div :class="{scrolA:true,scrolB:scrolB }" @dragover="dragover" @dragleave="dragleave" @drop="drop" >
           
            <progress class="pure-material-progress-linear" :style="{'width':'100%', 'position': 'absolute', 'top': spiner ? '35px': '-35px','z-index':'2'}"/>
            <label for="assetsFieldHandle" class="block cursor-pointer" style=" width: 100%;height: 100%;" v-if="filelist.length ==0">
                <div style="color: #AF3437; background: #fff;cursor: pointer;font-size: 16px;font-weight: 400;width: 100%;display: flex;height: 100%;align-items: center; justify-content: center;" >
                    <span style="padding:60px;" >Se preferir, arraste aqui os seus arquivos .XML e .ZIP  </span>            
                </div>
            </label>          
            <ul  v-cloak  class="ulDentro" >
                <li class="text-sm p-1" v-for="(file,i) in filelist" :key="i" style="display: flex;align-items: center;justify-content: space-between;" @click="remove(i)">
                    <div>{{file.name }}</div>
                    <a style="color:#AF3437;cursor: pointer;padding-right: 15px;">Excluir</a>
                </li>
            </ul>
        </div>
        </div>
    </div>
    <div style="display: flex; justify-content: center; margin-top: 15px;">
     <button @click="irParaPaginaConcluido" style="cursor: pointer; border: none; color: #FFFFFF; margin-top: 20px; width: 203px;height: 34px;left: 258px;top: 726px;background: #AF3437; border-radius: 5px;"> Finalizar Importação
         </button>  
        <p v-if="txtValidacao" style="margin-top: 25px; margin-left: 8px; color:red">{{txtValidacao}}</p>
  </div>
</div>
</template>

<script>
import {  mapMutations } from 'vuex';
export default {
data(){
  return{
    filelist : [],
    spiner : false,
    scrolB : false,
    respostaOp : false,
    txtValidacao:''
  }
},
methods : {
    ...mapMutations(['setFile','setPasso']),
    irParaPaginaConcluido(){
        this.txtValidacao= ''
        if(this.filelist.length == 0){//verifica se tem arquivo
            this.txtValidacao = 'Faça a importação do seu XML ou .ZIP'//exibi mensagem de erro
        }else{
            this.setPasso(3)
            this.setFile(this.filelist)
            this.$router.push({name:'concluido',params:{idEmpresa:this.$route.params.idEmpresa}})
        }
    },
  dragover(event) {
      event.preventDefault();
      if (!event.currentTarget.classList.contains('bg-green-300')) {
        event.currentTarget.classList.remove('bg-gray-100');
        event.currentTarget.classList.add('bg-green-300');
      }
    },
    dragleave(event) { 
      event.currentTarget.classList.add('bg-gray-100');
      event.currentTarget.classList.remove('bg-green-300');
    },
    drop(event) {
      event.preventDefault();
      this.$refs.file.files = event.dataTransfer.files;
      this.onChange(); 
      event.currentTarget.classList.add('bg-gray-100');
      event.currentTarget.classList.remove('bg-green-300');
    },
  onChange() {    
    this.txtValidacao = ''
        console.log(this.$refs.file.files)
        this.scrolB = true
        this.filelist = [...this.$refs.file.files];       
        this.passo = 2   
    },
    remove(i) {
      this.filelist.splice(i, 1);
      if(this.filelist.length ==0){         
          this.passo = 1;
          this.scrolB = false
      }
    },
}
}
</script>

<style>

li.text-sm.p-1 {
    font-size: 13px;
    width: 99.5%;
    list-style: none;
    background: #fff;
    display: flex;
    padding: 23px;
    height: 40px;
    border-radius: 5px;
    display: flex;
    padding-left: 20px;
    align-items: center;
    padding-left: 15px !important;
}
label {
    color: #7e7e7e;
    cursor: pointer;
    font-size: 14px;
    font-weight: 400;
}
li{
    color: #3e3e3e;
}
li  button{
    color: #1696e7;
    outline: medium none;
    background: #fff;
}
div.scrolB{
    border: 2px solid #AF3437;
}
.NotasEncontradas{
    background: #AF3437;
    cursor: pointer;
    width: 100%;
    height: 40px;
    margin-bottom: 0;
    display: flex;
    color: #fff;
    font-weight: bold;
    padding-left: 15px;
    align-items: center;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}
.scrolA::-webkit-scrollbar {
  width: 8px !important; 
}
.scrolA::-webkit-scrollbar-track {
  background-color: rgb(0, 0, 0, 0);
}
.scrolA::-webkit-scrollbar-thumb {
  background: #4e4e4e;
  border-radius: 25px;
}
.scrolA{
    position: relative;
border: 2px dashed #AF3437;
box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
    max-height:400px;overflow:auto;flex-direction: column;display: flex;border-radius: 8px;align-items:center;justify-content: center;
}
.ulDentro{
    padding: 0;
    display: flex;
    width: 100%;
    justify-content: center;
    flex-direction: column;
    align-items: center;     
    
}
.atePassoDois{
    position:relative;z-index:2;transition: 0.5s all;
    left: 0%;
}
.pure-material-progress-linear {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    border: none;
    height: 0.25em;
    color: #AF3437;
  
    font-size: 16px;
}

.pure-material-progress-linear::-webkit-progress-bar {
    background-color: transparent;
}

/* Determinate */
.pure-material-progress-linear::-webkit-progress-value {
    background-color: #AF3437;
    transition: all 0.2s;
}

.pure-material-progress-linear::-moz-progress-bar {
    background-color: #AF3437;
    transition: all 0.2s;
}

.pure-material-progress-linear::-ms-fill {
    border: none;
    background-color: #AF3437;
    transition: all 0.2s;
}

/* Indeterminate */
.pure-material-progress-linear:indeterminate {
    background-size: 200% 100%;
    background-image: linear-gradient(to right, transparent 50%, currentColor 50%, currentColor 60%, transparent 60%, transparent 71.5%, currentColor 71.5%, currentColor 84%, transparent 84%);
    animation: pure-material-progress-linear 2s infinite linear;
}

.pure-material-progress-linear:indeterminate::-moz-progress-bar {
    background-color: transparent;
}

.pure-material-progress-linear:indeterminate::-ms-fill {
    animation-name: none;
}

@keyframes pure-material-progress-linear {
    0% {
        background-size: 200% 100%;
        background-position: left -31.25% top 0%;
    }
    50% {
        background-size: 800% 100%;
        background-position: left -49% top 0%;
    }
    100% {
        background-size: 400% 100%;
        background-position: left -102% top 0%;
    }
}
</style>
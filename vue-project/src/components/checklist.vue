<template>
  <div id="checklist">
    <div class="cadastro-tarefa">
      <input class="cadastro-input" type="text" placeholder="Insira o nome da tarefa tarefa aqui." maxlength="20" v-model="cadastro"/>
      <div class="button-send" v-on:click="addItem">OK</div>
    </div>
    <div class="error-msg" v-if="error">A tarefa precisa ter pelo menos 5 letras.</div>
    <div class="list aguardo">
      <div class="list-title">Em aguardo</div>
      <div class="item-list" v-for="tarefa in tarefas" :key="tarefa.id">
        <div class="check" :itemId="tarefa.id" v-on:click="addToFeito">&#10004;</div>
        <div class="titulo-tarefa">{{tarefa.tarefa}}</div>
      </div>
    </div>
    <div class="list feitas">
      <div class="list-title">Feitas</div>
      <div class="item-list" v-for="tarefafeita in tarefasFeitas" :key="tarefafeita.id">
        <div class="check">&#10004;</div>
        <div class="titulo-tarefa">{{tarefafeita.tarefa}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Checklist',
  methods:{
    addItem: function(event) {
      if(this.cadastro.length >= 5){

        let max = 0;
        this.tarefas.forEach(item => {
          if (item.id > max) {
            max = item.id;
          }
        });

        let maxFeitas = 0;
        this.tarefasFeitas.forEach(item => {
          if (item.id > max) {
            max = item.id;
          }
        });

        let maxAll = maxFeitas >= max? maxFeitas : max;

        this.tarefas.push({id: maxAll + 1, tarefa: this.cadastro});
        this.cadastro = "";
        this.error = false;

      }else{
        this.error = true;
      }
    },
    addToFeito: function(event){

      var idToRemove = event.currentTarget.getAttribute('itemId');

      this.tarefasFeitas.push(this.tarefas.filter(function(item) {
          return item.id == idToRemove;
      })[0]);

      this.tarefas = this.tarefas.filter(function(item) {
          return item.id != idToRemove;
      });

      console.log(this.tarefas, this.tarefasFeitas);
    }
  },
  data () {
    return {
      tarefas:[
        {id: 1, tarefa: 'Tarefa exemplo 1'},
        {id: 2, tarefa: 'Tarefa exemplo 2'},
        {id: 3, tarefa: 'Tarefa exemplo 3'}
      ],
      tarefasFeitas:[
        {id: 0, tarefa: 'Tarefa exemplo 0'}
      ],
      cadastro: '',
      error: false,
      keys: 0
    }
  }
}
</script>

<style lang="scss">
    #checklist{
      width: 40%;
      margin-left: 30%;
      margin-top: 80px;

      .error-msg{
        color: #ca3aaa;
        font-family: Arial;
        font-size: 16px;
        padding: 10px 4px;
      }

      .cadastro-tarefa{
        display: flex;
        flex-wrap: wrap;

        .cadastro-input{
          width: calc(100% - 30px - 100px);
          font-size: 20px;
          padding: 15px;
          background-color: #39384e;
          border: none;
          color: white;
          border-radius: 10px;
        }

        .button-send{
          width: 90px;
          margin: 0px 0px 0px 10px;
          background: linear-gradient(153deg, rgba(233,88,255,1) 0%, rgba(118,0,164,1) 55%, rgba(0,168,255,1) 100%);
          color:white;
          text-align: center;
          font-family: Arial;
          padding-top: 16px;
          border-radius: 10px;
          cursor: pointer;
          font-size: 20px;

          &:hover{
            opacity: 0.8;              
          }

          &:active{
            opacity: 0.5;
          }
        }
      }

      .list{
        margin-top: 60px;

        .list-title{
          color:white;
          font-family: Arial;
          font-size: 26px;
          border-bottom: 2px solid white;
          width: unset;
          margin-bottom: 20px;
        }

        .item-list{
          display: flex;
          flex-wrap: wrap;
          background-color: #302f42;
          width: calc(100% - 20px);
          padding: 15px 10px;
          color:white;
          font-family: Arial;
          font-size: 22px;
          border-radius: 10px;
          margin: 10px 0px;

          .check{
            margin: 0px 30px 0px 10px;
            padding: 0px 6px;
            border-radius: 20%;
            position: relative;
            background-color: #302f42;
            z-index: 1;
            cursor: pointer;         

             &::after {
              content: '';
              position: absolute;
              top: 0; right: 0; bottom: 0; left: 0;
              z-index: -1;
              width: 31px;
              height: 31px;
              background: #302f42;
              border-radius: 20%;
            }            
          }

          .titulo-tarefa{
            transform: translateY(4px);
            letter-spacing: 1px;
          }
        }
      }

      .list.aguardo{
        .check{
             &:hover{
              color: rgba(233,88,255,1);

              &::before{             
                animation: changeBorder 0.85s infinite;
                animation-timing-function: ease-out;
                -webkit-animation-timing-function: ease-out;
                transition: 0.2;
              }
            }

            &::before {
              content: '';
              position: absolute;
              top: -2px; right: 0px; bottom: 0px; left: -2px;
              z-index: -1;
              width: 35px;
              height: 35px;
              background: white;
              border-radius: 20%;
            }
        }
      }

      .list.feitas{
        .check{      
            cursor: default;
            color: #1abdb7;

            &::before {
              content: '';
              position: absolute;
              top: -2px; right: 0px; bottom: 0px; left: -2px;
              z-index: -1;
              width: 35px;
              height: 35px;
              background: #1abdb7;
              border-radius: 20%;
            }
        }
      }
    }

    @keyframes changeBorder{
      0%{
              background: linear-gradient(153deg, rgba(233,88,255,1) 0%, rgba(118,0,164,1) 55%, rgba(0,168,255,1) 100%);
      }
      20%{
              background: linear-gradient(153deg, rgba(0,168,255,1) 0%, rgba(233,88,255,1) 55%, rgba(118,0,164,1) 100%);
      }

      40%{
              background: linear-gradient(153deg, rgba(118,0,164,1) 0%, rgba(0,168,255,1) 55%, rgba(233,88,255,1) 100%);
      }

      60%{
              background: linear-gradient(153deg, rgba(233,88,255,1) 0%, rgba(118,0,164,1) 55%, rgba(0,168,255,1) 100%);
      }

      80%{
              background: linear-gradient(153deg, rgba(0,168,255,1) 0%, rgba(233,88,255,1) 55%, rgba(118,0,164,1) 100%);
      }

      100%{
              background: linear-gradient(153deg, rgba(118,0,164,1) 0%, rgba(0,168,255,1) 55%, rgba(233,88,255,1) 100%);
      }
    }
</style>

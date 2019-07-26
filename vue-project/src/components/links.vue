<template>
  <div id="links">
    <a class="link" v-for="link in links" :href="link.link" v-bind:key="link.id">{{link.title}}</a>
  </div>
</template>

<script>
export default {
  name: 'Links',
  data () {
    return {
      links:[
        {id: 1, title: 'TAREFAS' , link: '#'},
        {id: 2, title: 'LINK 2' , link: '#'},
        {id: 3, title: 'VOLTAR', link: 'http://lucasmendoncapportfolio.atwebpages.com/'}
      ]
    }
  }
}
</script>

<style lang="scss">
    #links{
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        position: absolute;
        right: 40px;
        top: 15px;

        .link{
            color:white;
            font-family: arial;
            font-size: 18px;
            padding: 10px 15px;
            cursor: pointer;
            position: relative;
            letter-spacing: 2px;
            text-decoration: none;

            &:visited{
              opacity: 0.5;
            }

            &:hover{
                &:after{
                    content: '';
                    height: 3px;
                    width: calc(100% - 10px);
                    position:absolute;
                    background: white;
                    left: 5px;
                    bottom: 3px;
                    transition: 0.2s;
                    animation: Aparecer 0.4s;
                }
            }

            &:active{
                opacity: 0.6;
            }

        }
    }

    @keyframes Aparecer{
        0%{
            width: calc(0% - 10px);
            left: 50%;
        }

        100%{
            width: calc(100% - 10px);
            left: 5px;
        }

    }
</style>

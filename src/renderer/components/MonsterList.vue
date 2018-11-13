<template>
  <div id="wrapper">
    <div>
      <div class="kikendo">危険度2</div>
      <Monster v-for="monster in monsterList2"
      v-bind:name="monster.name"
      v-bind:HP="monster.HP"
      v-bind:count="monster.count"/>
      <div class="kikendo">危険度3</div>
      <Monster v-for="monster in monsterList3"
      v-bind:name="monster.name"
      v-bind:HP="monster.HP"
      v-bind:count="monster.count"/>
    </div>
  </div>
</template>

<script>
  import Monster from './Monster'

  export default {
    name: 'monster-list',
    components: { Monster },
    data(){
      return{
        monster:Monster,
        monsterList2:[],
        monsterList3:[]
      }
    },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
        console.log('hoge');
      },

      readJson (storage) {
        storage.get('config', function (error, data) {
            if (error) throw error;

            if (Object.keys(data).length === 0) {
                
                console.log('data nasi');
                // データがないときの処理
            } else {
                console.log(data);
                // データがあるときの処理
            }
        });
      },

      setJson(name,count){
        let setJson = {'name':name,'count':count}

        storage.set('config', setjson, function (error) {
            if (error) throw error;
        });
      }
    },
    mounted: function(){
      let monsterList2 = this.monsterList2;
      let monsterList3 = this.monsterList3;
      let monster = this.monster;
      const MONSTERJSON = [
        {
            "name":"レイギエナ",
            "kikendo":"2",
            "HP":"3000"
        },
        {
            "name":"オドガロン",
            "kikendo":"2",
            "HP":"3000"
        },{
            "name":"ウラガンキン",
            "kikendo":"2",
            "HP":"4300"
        },{
            "name":"リオレイア亜種",
            "kikendo":"2",
            "HP":"3000"
        },{
            "name":"リオレウス",
            "kikendo":"2",
            "HP":"3250"
        },{
            "name":"リオレウス亜種",
            "kikendo":"2",
            "HP":"3250"
        },{
            "name":"ディアブロス",
            "kikendo":"2",
            "HP":"3250"
        },{
            "name":"ディアブロス亜種",
            "kikendo":"2",
            "HP":"3450"
        },{
            "name":"バゼルギウス",
            "kikendo":"2",
            "HP":"4550"
        },{
            "name":"ヴォルガノス",
            "kikendo":"2",
            "HP":"4000"
        },{
            "name":"ネルギガンテ",
            "kikendo":"3",
            "HP":"3520"
        },{
            "name":"ヴァルハザク",
            "kikendo":"3",
            "HP":"4700"
        },{
            "name":"テオ・テスカトル",
            "kikendo":"3",
            "HP":"4300"
        },{
            "name":"クシャルダオラ",
            "kikendo":"3",
            "HP":"3980"
        }
      ];

      
      const storage = require('electron-json-storage');

      this.readJson(storage);

      for(let temp of MONSTERJSON){
        //console.log(temp.name);
        if(temp.kikendo=="2"){
          monsterList2.push({name:temp.name,HP:Number(temp.HP),count:0});
        }else{
          monsterList3.push({name:temp.name,HP:Number(temp.HP),count:0});
        }
      }
    }
  }
</script>

<style>

</style>

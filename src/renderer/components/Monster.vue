<template>
  <div class="wrapper">
      <div class="monster-name">{{  name  }}</div>
      <div class="monster-HP">HP{{  HP  }}</div>
      <div class="monster-count">4枠{{  count  }}回</div>
      <button @click="countUp(name,count)">+</button>
      <button @click="countDown(name,count)">-</button>
  </div>
</template>

<script>
  export default {
    name: 'monster-list',
    props:{
      name:String,
      count:Number,
      HP:Number
    },
    methods:{
      countUp(name,count){
        this.count=count+1;
        this.setJson(name,count);
      },
      countDown(name,count){
        this.count=count-1;
        this.setJson(name,count);
      },
      setJson(name,count){
        let setJson = [{'name':name,'count':count}];
        
        const storage = require('electron-json-storage');

        this.readJson(storage).
          then(function(saveData){console.log(saveData)});

        storage.set('config', setJson, function (error) {
            if (error) throw error;
        });
      },
      readJson (storage) {
        storage.get('config', function (error, data) {
            if (error) throw error;

            if (Object.keys(data).length === 0) {
                
                console.log('data nasi');
                // データがないときの処理
            } else {
              console.log(data);
                return data;
            }
        });
      },

    }
  }
</script>

<style>
  .wrapper{
    display:flex;
    border:1px solid;
    margin-bottom:5px;
  }
  .monster-name{
    width:150px;
  }

  .monster-HP{
    margin-left:10px;
  }

  .monster-count{
    margin-left:10px;
  }
</style>

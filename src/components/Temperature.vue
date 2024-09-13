<script>

  export default {
    data() {
      return {
        cent: 0,
        fahren: 32,   
      };
    },
    watch:{
      cent(newVal){
        this.fahren=((newVal*(9/5))+32).toFixed(1)
      },
        fahren(newVal){
        this.cent=((newVal-32)*5/9).toFixed(1)
      },
    }
  };
</script>

<template>
    <div class="temperature-container">
    
        <form id='calculate'>
            <label>Celsius<br>
            <input  v-model.number='cent' type='number'>
            <small v-show="cent < -30 || cent > 200">The temparature range allowed is between -30°C and 200°C</small>
            </label>
            <div class="calc-celsius">
            
                <ul>
                    <li v-for="index in 231">
                        <span v-if="(index-1) % 10 == 0">{{ index-31 }}</span>
                        
                    </li>
                </ul>
            </div>
            <div class="calc-temp">
                <ul class="temparature-img">
                    <li v-for="index in 231"
                        :class="{ 'up' : cent > (index-31) && (index-30) > 0, 'down' : cent < (index-30) && (index-31) < 0 }">
                    </li>
                </ul>
            </div>
            <div class="calc-fahrenheit">
                <ul>
                    <li v-for="index in 231">
                        <span v-if="(index-1) % 10 == 0">{{ (((index-31) * 9/5) + 32).toFixed(1) }}</span>
                        
                    </li>
                </ul>

            </div>
            <label>Fahrenheit<br>
            <input  v-model.number='fahren' type='number' >
            </label>
        </form>
    </div>
</template>

<style scoped>
    .temperature-container form {
        display: flex;
    }
    .temperature-container form label {
        min-width: 250px;
        text-align: center;
    }
    .temperature-container form label small {
        color: red;
        font-style: italic;
        display: block;
    }
    .temperature-container ul li {
        height: 3px;
        position: relative;
        text-align: center;
        width: 50px;
    }
    .temperature-container ul li span {
        position: absolute;
        top: 0;
        left: 0;
        font-size: 10px;
        line-height: 10px;
    }
    .temperature-container ul li:has(> span) {
      border-top: 1px solid black;
    }
    .temperature-container .temparature-img .up {
        background-color: red;
    }
    .temperature-container .temparature-img li {
        border-left: 1px solid black;
        border-right: 1px solid black;
    }
    .temperature-container .temparature-img .down {
        background-color: blue;
    }
</style>

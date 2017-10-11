<template>
  <div id="app">
    <div style="text-align:center">
      格子数: <select name="" id="" v-model.number='gridNum'>
        <option value=4>4</option>
        <option value=5>5</option>
        <option value=6>6</option>
        <option value=7>7</option>
        <option value=8>8</option>
      </select>
      <br />
      <br />
      数字键盘: <select name="" id="" v-model='isNumber'>
        <option value=true>是</option>
        <option value=false>否</option>
      </select>
      <br />
      <br />
      显示密码: <select name="" id="" v-model='isPassword'>
        <option value=false>是</option>
        <option value=true>否</option>
      </select>
      <br /> 
      <br /> 
      <br />
      <button @click='show=true'>调出输入框</button> 
    </div>
    <GridPassword
     v-if='show' 
     :passwordLength='gridNum' 
     :onConfirm='onConfirm' 
     :onClose='onClose' 
     :isNumber='isNumber | formatBool'
     :isPassword='isPassword | formatBool'
     :isBtn='isBtn'></GridPassword>
  </div>
</template>

<script>
import GridPassword from '@/components/GridPassword'

export default {
  name: 'app',
  data() {
    return {
      show:false,
      gridNum: 4,
      isNumber:true,
      isPassword:true,
      isBtn:true,
      onConfirm: (e) => {
        this.show = false
        alert(e);
      },
      onClose: () => {
        this.show = false
      }
    }
  },
  components: {
    GridPassword
  },
  filters: {
    formatBool(value) {
      switch(value) {
        case 'true':return true;break;
        case 'false':return false;break;
      }
    }
  }
}
</script>

<template>
  <div class="pop" v-if='showPanel' @click='focusInput()'>
    <input
     v-if='isNumber'
     class="hidden_input"
     type="tel"
     style="margin-left:9999999px" 
     ref="hiddenInput" 
     @input="controlInput" 
     v-model="hiddenInput" />
    <input
     v-else
     class="hidden_input"
     type="text" 
     style="margin-left:9999999px" 
     ref="hiddenInput" 
     @input="controlInput" 
     v-model="hiddenInput" />
     <div class="wrap">
       <div class="tip">{{tip}}</div>
      <div class="input_list" v-if='isPassword'>
        <input
         v-for='(item, index) in passwordLength'
         :value='hiddenInput.substring(index, index+1)'
         class="input_grid"
         :style='{width:(2.5-(passwordLength-4)*0.3)+"em", height: (2.5-(passwordLength-4)*0.3)+"em"}'
         type="password" 
         disabled='true' />
      </div>
      <div class="input_list" v-else>
        <input
         v-for='(item, index) in passwordLength'
         :value='hiddenInput.substring(index, index+1)'
         class="input_grid"
         :style='{width:(2.5-(passwordLength-4)*0.3)+"em", height: (2.5-(passwordLength-4)*0.3)+"em"}'                   
         type="text" 
         disabled='true' />
      </div>
      <div class="btn_list" v-if='isBtnCtr'>
        <button class="btn" @click='cancel'>取消</button>
        <button class="btn btn_confirm" @click='confirm'>确认</button>
      </div>
     </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        showPanel: true,
        hiddenInput: ""
      }
    },
    mounted() {
      this.focusInput()
    },
    computed: {
    },
    methods: {
      controlInput() {
        if(this.hiddenInput.length == this.passwordLength && !this.isBtnCtr) {
            this.onConfirm(this.hiddenInput)
            this.showPanel = false
        }
        if(this.hiddenInput.length > this.passwordLength) {
            this.hiddenInput = this.hiddenInput.slice(0, this.passwordLength)
        }
      },
      focusInput() {
        this.$refs.hiddenInput.focus()
      },
      cancel(e) {
        e.stopPropagation()
        this.showPanel = false
      },
      confirm(e) {
        e.stopPropagation()
        if(this.hiddenInput.length == this.passwordLength) {
            this.onConfirm(this.hiddenInput)
            this.showPanel = false
        }else {
          this.focusInput()
        }
      }
    },
    props: {
      tip: {
        type: String,
        default: '请输入密码',
        require: false
      },
      passwordLength: {
        type: Number,
        default: 6,
        require: false,
        validator: function (value) {
          return value % 1 === 0 && value >= 4 && value <= 8
        }
      },
      isPassword: {
        type: Boolean,
        default: true,
        require: false
      },
      isNumber: {
        type: Boolean,
        default: true,
        require: false
      },
      isBtnCtr: {
        type: Boolean,
        default: true,
        require: false
      },
      onConfirm: {
        type: Function,
        require: true
      }
    }
  }
</script>

<style scoped>
  .pop {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1000;
    background-color: rgba(0, 0, 0, 0.4);
  }
  .hidden_input {
    position: absolute; 
    opacity: 0; 
    filter:Alpha(opacity=0);
  }
  .wrap {
    width: 80vw;
    padding: 20px;
    border-radius: 5px;
    background-color: #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -100%);
  }
  .tip {
    text-align: center;
    padding: 5px;
  }
  .input_list {
    display: flex;
    justify-content: space-between;
    margin-top: 15px;
  }
  .input_grid {
    line-height: 1;
    text-align: center;
    border: 1px solid #000;
    border-radius: 5px;
    background-color: #f4f4f4;
    font-size: 100%;
    color: #000;
    opacity: 1;
  }
  .btn_list {
    margin-top: 30px;
    padding: 0px 50px;
    display: flex;
    justify-content: space-around;
  }
  .btn {
    line-height: 1;
    white-space: nowrap;
    text-align: center;
    box-sizing: border-box;
    outline: none;
    padding: 10px 15px;
    font-size: 14px;
    border-radius: 4px;
    border: 1px solid #bfcbd9;
    border-color: #c4c4c4;
    background-color: #fff;
  }
  .btn:active {
    color: #1d90e6;
    border-color: #1d90e6;
  }
  .btn_confirm {
    color: #fff;
    background-color: #20a0ff;
    border-color: #20a0ff;
  }
  .btn_confirm:active {
    background-color: #4db3ff;
  }
</style>

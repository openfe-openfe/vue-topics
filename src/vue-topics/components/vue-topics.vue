<template>
  <div class="tag-input form-control d-inline-block bg-white py-0">
    <ul class="js-tag-input-selected-tags d-inline">
      <li class="topic-tag-action f6 float-left js-tag-input-tag js-template" v-show="topics.length > 0" v-for="item in topics">
        <span class="js-placeholder-tag-name">{{item}}</span>
        <button type="button" class="delete-topic-button f5 no-underline ml-2 js-remove" @click="delTopics(item)">
          ×
        </button>
        <input type="hidden" name="repo_topics[]" class="js-topic-input" value="">
      </li>
    </ul>
    <input type="text" id="repo_topics" class="tag-input-inner form-control bg-white shorter d-inline-block p-0 my-1 border-0" autocomplete="off" autofocus=""
      placeholder="标签用回车分隔"
      v-model="inputVal"
      @keydown.enter="enterTopics"
      @keydown="delectCode"
    />
  </div>
</template>

<script>
export default {
  data () {
    return {
      topics: [],
      inputVal: ''
    }
  },
  created() {
    this.$watch('inputVal', newQuery => {
        this.inputVal = newQuery
    })
  },
  methods : {
    // 添加标签
    enterTopics() {
      // 添加之前先拿到数组之前的值，判断如果有重复就不会添加
      let arr = this.topics
      let inputVal = this.inputVal
      if(inputVal!= '') {
        const compare = (item) => {
          return item === inputVal
        }
        const index = arr.findIndex(compare) // 传入比较函数
        // console.log(index)
        // if (index === 0) {
        //   return
        // }
        if (index >= 0) {
          arr.splice(index, 1)
        }
        arr.push(inputVal)
        // 这个时候该清空input的值了
         this.inputVal = ''
      }
    },
    delTopics(val) {
      // 检查数组中如果存在，就删除
      let arr = this.topics
      let delVal = val
      const compare = (item) => {
        return item === delVal
      }
      const index = arr.findIndex(compare) // 传入比较函数
      if (index > -1) {
        this.topics.splice(index, 1)
        this.inputVal = ''
      }
    },
    delectCode(ev) {
      // console.log(ev)
      if(ev.key === 'Backspace') {
        if(this.inputVal == '') {
          // 如果值不为空的话 ，那么就是挨个删除
          this.topics.pop()
        }
      }
    }
  }
}
</script>

<style>
  * {
      box-sizing: border-box;
  }
  body.intent-mouse [role="button"]:focus, body.intent-mouse button:focus, body.intent-mouse summary:focus {
      outline: none;
  }
  button, select {
      outline: none;
      text-transform: none;
  }
  button, input {
      overflow: visible;
  }
  button, input, select, textarea {
      font: inherit;
      margin: 0;
  }
  .tag-input {
    width: 908px;
    cursor: text;
    overflow: auto;
  }
  .bg-white {
    background-color: #fff !important;
  }
  .form-control {
    min-height: 34px;
    padding: 6px 8px;
    font-size: 16px;
    line-height: 20px;
    color: #24292e;
    vertical-align: middle;
    background-color: #fff;
    background-repeat: no-repeat;
    background-position: right 8px center;
    border: 1px solid #d1d5da;
    border-radius: 3px;
    outline: none;
    box-shadow: inset 0 1px 2px rgba(27,31,35,0.075);
  }
  .tag-input ul {
    list-style: none;
  }
  .d-inline {
    display: inline !important;
  }
  .topic-tag-action {
    display: inline-flex;
    align-items: center;
    padding-left: 0.8em;
    margin: 0.4em 0.4em 0 0;
    background-color: #f1f8ff;
    border-radius: 3px;
  }
  .d-none {
    display: none !important;
  }
  .f6 {
    font-size: 12px !important;
  }

  .float-left {
    float: left !important;
  }

  button, html [type="button"], [type="reset"], [type="submit"] {
    -webkit-appearance: button;
  }
  .delete-topic-button {
    display: inline-block;
    width: 26px;
    color: #6a737d;
    background-color: #f1f8ff;
    border-top: 0;
    border-right: 0;
    border-bottom: 0;
    border-left: 1px solid #b4d9ff;
    border-top-right-radius: 3px;
    border-bottom-right-radius: 3px;
  }
  .delete-topic-button:hover {
     background-color: rgb(225,237,254);
      border-left: 1px solid rgb(225,237,254);
  }
  .no-underline {
    text-decoration: none !important;
  }
  .f5 {
    font-size: 14px !important;
  }
  .ml-2 {
    margin-left: 8px !important;
  }
  button {
    cursor: pointer;
    border-radius: 0;
  }
  .tag-input input {
    float: left;
    padding-left: 2px;
    margin: 0;
    background: none;
    border: 0;
    box-shadow: none;
  }
  .tag-input .tag-input-inner {
    min-height: 26px;
  }
  .form-control.shorter {
      width: 130px;
  }
  .tag-input input {
    float: left;
    padding-left: 2px;
    margin: 0;
    background: none;
    border: 0;
    box-shadow: none;
  }
  .d-inline-block {
    display: inline-block !important;
  }
  .p-0 {
    padding: 0 !important;
  }
  .py-0 {
    padding-top: 0 !important;
    padding-bottom: 0 !important;
  }
  .my-1 {
    margin-top: 4px !important;
    margin-bottom: 4px !important;
  }
  .bg-white {
    background-color: #fff !important;
  }
  .border-0 {
    border: 0 !important;
  }
</style>



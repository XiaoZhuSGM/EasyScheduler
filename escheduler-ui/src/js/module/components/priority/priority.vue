<template>
  <div class="priority-model">
    <x-select @on-change="_onChange" v-model="value" style="width: 130px;" :disabled="isDetails">
      <div slot="trigger" slot-scope="{ selectedModel }" class="ans-input" >
        <div class="input-element" :class="isDetails?'disabled' : ''">
          <span v-html="_rtUnicode(selectedModel ? selectedModel.label : 'MEDIUM')"></span>
          <span class="label-p">{{selectedModel ? selectedModel.label : 'MEDIUM'}}</span>
          <i class="ans-icon-arrow-down" ></i>
        </div>
      </div>
      <x-option
              v-for="item in priorityList"
              :key="item.code"
              :value="item.code"
              :label="item.code">
        <li class="ans-option ans-option-listp">
          <span class="default-option-class">
            <i class="iconfont" v-html="item.unicode" :style="{color:item.color}"></i>
            {{item.code}}
          </span>
        </li>
      </x-option>
    </x-select>
  </div>
</template>
<script>
  import _ from 'lodash'
  import disabledState from '@/module/mixin/disabledState'

  export default {
    name: 'priority',
    data () {
      return {
        priorityList: [
          {
            code: 'HIGHEST',
            unicode: '&#xe632;',
            color: '#ff0000'
          },
          {
            code: 'HIGH',
            unicode: '&#xe632;',
            color: '#ff0000'
          },
          {
            code: 'MEDIUM',
            unicode: '&#xe632;',
            color: '#EA7D24'
          },
          {
            code: 'LOW',
            unicode: '&#xeef8;',
            color: '#2A8734'
          },
          {
            code: 'LOWEST',
            unicode: '&#xeef8;',
            color: '#2A8734'
          }
        ]
      }
    },
    props: {
      value: {
        type: String,
        default: 'MEDIUM'
      }
    },
    mixins: [disabledState],
    model: {
      prop: 'value',
      event: 'priorityEvent'
    },
    methods: {
      _rtUnicode (value) {
        let o = _.find(this.priorityList, ['code', value])
        return `<i class="iconfont" style="color:${o.color}">${o.unicode}</i>`
      },
      _onChange (o) {
        this.value = o.value
        this.$emit('priorityEvent', o.value)
      }
    },
    created () {
    },
    mounted () {
    },
    components: {}
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  .priority-model {
    .ans-option-listp {
      >span {
        font-weight: normal;
        >.iconfont {
          padding-right: 2px;
        }
      }
    }
    .ans-input {
      .input-element {
        cursor: pointer;
        height: 32px;
        line-height: 30px;
        position: relative;
        font-weight: normal;
        .ans-icon-arrow-down {
          position: absolute;
          right: 8px;
          top: 0;
          font-size: 12px;
          color: #888;
          cursor: pointer;
        }
        span {
          vertical-align: middle;
          &.label-p {
            margin-top: -4px;
            display: inline-block;
          }
        }
      }
    }
  }
</style>

<template>
    <div class="table-auto">
        <div class="table-title">
          <span>{{id.title}}</span>
        </div>
        <div class="scroll-box">
          <a-table
            class="table-scroll"
            :style="{top}"
            :columns="columns"
            :rowKey="(record,index) => record.telphoneNum+index"
            :dataSource="tableData"
            :pagination="false"
            :showHeader="true"
            >
            <span slot="status" slot-scope="status, record">
              <a-tag
                v-for="tag in status"
                :key="tag"
                :class="status-tag"
                :color="tag === '1' ? '#24C768' : tag === '-1'? '#D70907' : '#F8B551'"
              >
              </a-tag>
              {{record.status[0] === '1' ? '正常' : record.status[0] === '-1'? '问题' : '断点'}}
            </span>
          </a-table>
        </div>
    </div>
</template>
<script>
export default {
  name: "tableAuto",
  props: ['tableDatas', 'ids','columns','heights'],
  data() {
    return {
      todos: [],
      initData: this.tableDatas,
      tableData: this.tableDatas,
      id: this.ids,
      column: this.columns,
      activeIndex: 0,
      view:'',
      height: this.heights
    };
  },
  computed: {
    top() {
      return -this.activeIndex * 25 + "px"+`;height:${this.height/2}`;
    },

  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      var n = setInterval( () => {
        var circle = this.autoScroll()
      },1000)
      
    },
    autoScroll() {
      let time = this.activeIndex%5 === 0 ? 6000: 1000
      var a = setInterval(_ => {
          let free = Math.floor(Math.random()*12)+1;
          this.tableData = this.tableData.concat(this.initData[free]||[]);
          if (
            this.activeIndex <
            this.tableData.length
          ) {
            this.activeIndex += 1;
          }else {
            this.activeIndex = 0
          }
          this.tableData.shift()
          clearInterval(a)
      }, time);
      
    },
  }
}
</script>
<style lang="less">
  .table-auto {
    font-size: 12px;
    position: relative;
    overflow: hidden;
    .table-title {
      text-align: left;
      span {
          line-height: 40px;
          font-size: 14px;
          font-weight: 600;
          font-family: sans-serif;
          letter-spacing: 2px;
          background: linear-gradient(to right, #76e6db, #6483bd);
          -webkit-background-clip: text;
          color: transparent;
      }
    }
    .scroll-box {
      overflow: hidden;
      height: 280px;
    }
    .table-scroll {
      position: relative;
      transition: top  0.825s;
      tbody {
        tr:nth-child(even) {  
            // background: #;  
        }  
        tr:nth-child(odd) {  
            background: #0E3B8C;  
        }  
      }
    }
    tr {
      border-bottom: 1px dashed #484444 ;
    }
    .table-td {
      color: #7CA3D0;
      padding: 8px 4px;
      background: transparent;
      font-size: 12px;
      border: none;
    }
    .ant-tag {
        height: 4px;
        border-radius: 0px;
    }
  }
</style>
<template>
  <div>
    <div class="tree-container" style="background-color:#fff;">
      <div class="tree-search">
        <el-row>
          <el-col :span="12">
            <el-row>
              <el-col :span="24">
                <el-input placeholder="输入关键字" v-model="filterText"></el-input>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="24">
                <el-tree class="filter-tree tree-modal" :data="dataarr" :props="defaultProps" node-key="id" default-expand-all :filter-node-method="filterNode"
                  :default-checked-keys='defaultchecked' ref="tree" show-checkbox @check-change="getCheckNode">
                </el-tree>
              </el-col>
            </el-row>
          </el-col>
          <el-col :span="12">
            <el-row>
              <el-col :span="24">
                <div class="title">已选用户:</div>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="24" class="sel-tree-list">
                <ul>
                  <li v-for="(item,index) in seltree" v-if="seltree.length!=0"><span>{{item.label}}</span><i @click="delRow(item,index)">&times;</i></li>
                </ul>
              </el-col>
            </el-row>
          </el-col>
        </el-row>
      </div>
      <el-row class="btn-submit">
        <el-col :span="24">
          <el-button type="primary" @click="submitData">提交</el-button>
          <el-button @click="closeModal" v-show="visibledismiss">取 消</el-button>
        </el-col>
      </el-row>
      <div v-show="false">{{getdata}}</div>
    </div>
  </div>

</template>
<script>
  // import echarts from "echarts";
  export default {
    data() {
      return {
        dialogFormVisible: false,
        filterText: "",
        seltree: [],
        defaultProps: {
          children: "children",
          label: "label"
        },
      };
    },
    props: {
      dataarr: {//初始数据
        type: Array,
        default() {
          return [];
        }
      },
      defaultchecked: {//已经保留在数据库中的数据，即已选中数据
        type: Array,
        default() {
          return [];
        }
      },
      defaultsel: {
        type: Array,
        default() {
          return [];
        }
      },
      visibledismiss:{
        type:Boolean,
        default(){
          return false;
        }
      }
    },

    watch: {
      filterText(val) {
        this.$refs.tree.filter(val);
      }
    },
    computed: {
      getdata() {
        this.seltree = this.defaultsel;
        // return;
      }
    },
    methods: {
      delUser(tag, index) {
        this.$emit("del-user", tag);
      },
      closeModal(){
        this.$emit("close-modal");
      },
      delRow(item, index) {
        this.seltree.splice(index, 1);
        this.$refs.tree.setChecked(item.id, false);
      },
      filterNode(value, data) {
        if (!value) return true;
        return data.searchtext.indexOf(value) !== -1;
      },
      getCheckNode() {
        this.seltree = this.$refs.tree.getCheckedNodes(true);
      },
      submitData() {
        this.$emit("tree-submit", this.seltree);
      }
    }
  };

</script>
<style scoped>
  .el-tree {
    border: none;
    overflow: auto;
    height: 300px;
  }
  
  .author-user-contain {
    padding: 10px;
    max-height: 90px;
    overflow: auto;
  }
  
  .author-user-contain .el-tag {
    margin: 0 10px 10px 0;
  }
  
  .tree-search {
    border-top: 1px solid #ddd;
    border-bottom: 1px solid #ddd;
    padding: 10px;
  }
  
  .tree-search>.el-row>.el-col {
    padding: 10px;
  }
  
  .tree-search>.el-row>.el-col:first-child {
    border-right: 1px solid #ddd;
  }
  
  .tree-modal {
    padding: 10px;
  }
  
  .sel-tree-list {
    height: 300px;
    overflow: auto;
    border: 1px solid #ddd;
    background-color: #f5f5f5;
  }
  
  .sel-tree-list li {
    position: relative;
    padding: 10px;
  }
  
  .sel-tree-list li>i {
    position: absolute;
    right: 10px;
    width: 15px;
    height: 15px;
    border-radius: 15px;
    line-height: 15px;
    text-align: center;
    background-color: #ddd;
    cursor: pointer;
  }
  .title {
    font-size: 14px;
    line-height: 36px;
  }
  .btn-submit{
    text-align: right;
    padding:10px 20px;;
  }
</style>
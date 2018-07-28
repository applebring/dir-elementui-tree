<template>
  <div>
    <div class="title">自定义基于elementui的树图组件</div>
    <div class="tree-container">
      <dir-tree :dataarr="data" :defaultchecked='defaultChecked' :defaultsel="defaultsel" @tree-submit="submitData" :visibledismiss="false"></dir-tree>
    </div>
    <el-button type="primary" @click="openModal">通过模态框打开</el-button>
    <el-dialog title="树图组件" :visible.sync="outerVisible">
      <dir-tree :dataarr="data2" :defaultchecked='defaultChecked2' :defaultsel="defaultsel2" @tree-submit="submitData2" @close-modal="closeModal" :visibledismiss="true"></dir-tree>
    </el-dialog>
  </div>

</template>


<script>
import dirTree from "../plugin/dirtree.vue";
//必备属性：dataarr(加载树图的数据) defaultchecked(树图加载默认选中项)
export default {
  data() {
    return {
      data: [
        {
          id: 1,
          label: "一级 1",
          searchtext: "一级1",
          children: [
            {
              id: 4,
              label: "二级 1-1",
              searchtext: "一级1二级1-1",
              children: [
                {
                  id: 9,
                  label: "三级 1-1-1",
                  searchtext: "一级1二级1-1三级1-1-1"
                },
                {
                  id: 10,
                  label: "三级 1-1-2",
                  searchtext: "一级1二级1-1三级1-1-2"
                }
              ]
            }
          ]
        },
        {
          id: 2,
          label: "一级 2",
          searchtext: "一级2",
          children: [
            {
              id: 5,
              label: "二级 2-1",
              searchtext: "一级2二级2-1"
            },
            {
              id: 6,
              label: "二级 2-2",
              searchtext: "一级2二级2-2"
            }
          ]
        },
        {
          id: 3,
          label: "一级 3",
          searchtext: "一级3",
          children: [
            {
              id: 7,
              label: "二级 3-1",
              searchtext: "一级3二级3-1"
            },
            {
              id: 8,
              label: "二级 3-2",
              searchtext: "一级3二级3-2"
            }
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      },
      defaultChecked: [7, 8], //选中项节点id
      defaultsel: [
        {
          id: 7,
          label: "二级 3-1",
          searchtext: "一级3二级3-1"
        },
        {
          id: 8,
          label: "二级 3-2",
          searchtext: "一级3二级3-2"
        }
      ], //右边框选中选项
      outerVisible: false,
      data2: [
        {
          id: 1,
          label: "一级 1",
          searchtext: "一级1",
          children: [
            {
              id: 4,
              label: "二级 1-1",
              searchtext: "一级1二级1-1",
              children: [
                {
                  id: 9,
                  label: "三级 1-1-1",
                  searchtext: "一级1二级1-1三级1-1-1"
                },
                {
                  id: 10,
                  label: "三级 1-1-2",
                  searchtext: "一级1二级1-1三级1-1-2"
                }
              ]
            }
          ]
        }
      ],
       defaultChecked2: [9], //选中项节点id
       defaultsel2:[
          {
                  id: 9,
                  label: "三级 1-1-1",
                  searchtext: "一级1二级1-1三级1-1-1"
                }
       ]
    };
  },
  components: { dirTree },
  methods: {
    submitData(data) {
      //参数data返回选中的子节点对象数组([{},{}])
      console.log("data", data);
      //服务器数据处理
    },
    openModal() {
      this.outerVisible = true;
    },
    closeModal(){
      this.outerVisible = false;
    }
  }
};
</script>
<style scoped>
.title {
  padding: 50px 0;
  text-align: center;
  background: #88d8f6;
  background: -webkit-gradient(
    linear,
    left top,
    right top,
    color-stop(0, #6babfb),
    color-stop(1, #88d8f6)
  );
  background: -ms-linear-gradient(right, #6babfb, #88d8f6);
  background: -o-linear-gradient(#88d8f6, #6babfb);
  filter: progid:DXImageTransform.Microsoft.gradient(
      startColorstr="#88D8F6",
      endColorstr="#6BABFB",
      GradientType=0
    );
  background: linear-gradient(to right, #6babfb, #88d8f6);
  box-shadow: none;
  color: #fff;
  font-size: 36px;
}
.tree-container {
  border: 1px solid #ddd;
  padding: 30px 100px;
  background-color: #e7e8e8;
}
.sub-title {
  font-size: 16px;
  font-weight: bolder;
}
</style>
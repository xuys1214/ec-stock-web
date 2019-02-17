<template>
  <section>
    <el-button type="text" @click="dialogFormVisible = true">打开嵌套表单的 Dialog</el-button>

    <el-dialog :visible.sync="dialogFormVisible" title="收货地址">
      <div class="dialog-wrapper">
        <div
          v-for="(item,key) in dlgItems"
          :key="key"
          class="dialog-item">
          <!--Input控件-->
          <div v-if="item.type=='input'">
            <label>{{ item.name }}</label>
            <el-input
              v-model="item.value"
              placeholder="请输入内容"
              prefix-icon="el-icon-search"/>
          </div>

          <!--InputNumber控件-->
          <div v-if="item.type=='input-number'">
            <label>{{ item.name }}</label>
            <el-input-number
              v-model="item.value"
              :min="item.min"
              :max="item.max"
              controls-position="right"/>
          </div>

          <!--Select控件-->
          <div v-if="item.type=='select'">
            <label>{{ item.name }}</label>
            <el-select v-model="item.value" filterable placeholder="请选择">
              <el-option
                v-for="op in item.options"
                :key="op.value"
                :label="op.label"
                :value="op.value"/>
            </el-select>
          </div>
        </div>

      </div>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </section>
</template>

<script>
export default {
  data() {
    return {
      dlgItems: [{
        type: 'input',
        name: 'test',
        value: 100
      },
      {
        type: 'input-number',
        name: 'test1',
        value: 1002,
        max: 1005
      },
      {
        type: 'select',
        name: 'selsect',
        options: [{
          value: '选项1',
          label: '黄金糕'
        }, {
          value: '选项2',
          label: '双皮奶'
        }, {
          value: '选项3',
          label: '蚵仔煎'
        }, {
          value: '选项4',
          label: '龙须面'
        }, {
          value: '选项5',
          label: '北京烤鸭'
        }]
      }],

      gridData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }],
      dialogTableVisible: false,
      dialogFormVisible: false,
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      formLabelWidth: '120px'
    }
  }
}
</script>

<style>
.el-dialog__body {
    padding: 10px 20px 10px 20px;
}
.dialog-wrapper {
    padding: 0 0 0 0;
}
.dialog-item {
    padding: 8px 0 8px 0;
}
.dialog-item label {
    text-align: right;
    vertical-align: middle;
    float: left;
    color: #606266;
    padding: 0 12px 0 0;
    box-sizing: border-box;
    width: 120px;
    height: 28px;
    line-height: 28px;
}
.dialog-item::before, .dialog-item::after  {
    display: table;
    content: "";
}
.dialog-item .el-input {
    width: 460px;
}
.dialog-item .el-input__inner {
    height: 28px;
    line-height: 28px;
}
.dialog-item .el-input-number .el-input {
    width: 180px;
}
.dialog-item .el-input-number, .el-input__prefix i {
    height: 28px;
    line-height: 28px;
}
.el-input-number.is-controls-right .el-input-number__decrease, .el-input-number.is-controls-right .el-input-number__increase {
    line-height: 8px;
}
.el-input__icon {
    line-height: 28px;
}

</style>

<template>
  <section>
    <el-dialog :visible.sync="dlgVisible" :title="title">
      <div class="dialog-wrapper">
        <div
          v-for="(item,key) in data"
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

          <!--DateTimePicker-->
          <div v-if="item.type=='dateTimePicker'">
            <label>{{ item.name }}</label>
            <el-date-picker
              v-model="item.value"
              :picker-options="item.options"
              type="datetimerange"
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
              align="right"/>
          </div>
        </div>

      </div>
      <div slot="footer" class="dialog-footer">
        <el-button @click="closeDialog()">取 消</el-button>
        <el-button type="primary" @click="save()">确 定</el-button>
      </div>
    </el-dialog>
  </section>
</template>

<script>
export default {
  props: {
    title: {
      default: '新增',
      type: String
    },
    data: {
      default() {
        return []
      },
      type: Array
    },
    dlgVisible: {
      default: false,
      type: Boolean
    }
  },
  data() {
    return {

    }
  },
  methods: {
    closeDialog() {
      this.$emit('cancle', false)
    },
    save() {
      this.$emit('save', this.data)
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
.el-date-editor .el-range__icon {
  line-height: 14px;
}
.el-date-editor .el-range-separator {
  line-height: 22px;
}

</style>

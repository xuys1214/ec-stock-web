<template>
  <div class="app-container">
    <div class="query-wrapper">
      <div class="app-query">
        <div class="query-item">
          <label>关键字</label>
          <el-input
            v-model="q_keyword"
            placeholder="请输入内容"
            prefix-icon="el-icon-search"/>
        </div>
        <div class="query-item">
          <label>可用额度</label>
          <el-input-number
            v-model="q_available"
            :min="0"
            controls-position="right"
          />
        </div>
        <div class="query-item">
          <label>信用额度</label>
          <el-input-number
            v-model="q_credit"
            :min="0"
            controls-position="right"
          />
        </div>
        <div class="query-item">
          <label>注册时间</label>
          <el-date-picker
            v-model="p_create"
            :picker-options="pickerOptions"
            type="datetimerange"
            range-separator="至"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            align="right"/>
        </div>
        <div class="query-item">
          <label>状态</label>
          <el-select v-model="q_status" filterable placeholder="请选择">
            <el-option
              v-for="item in q_status_options"
              :key="item.value"
              :label="item.label"
              :value="item.value"/>
          </el-select>
        </div>
        <div class="query-btn">
          <el-button type="primary" icon="el-icon-search">搜索</el-button>
        </div>
      </div>
    </div>
    <el-table
      v-loading="listLoading"
      ref="multipleTable"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row
      @selection-change="handleSelectionChange">
      <el-table-column type="selection" width="55"/>
      <el-table-column align="center" label="ID" width="95">
        <template slot-scope="scope">
          {{ scope.$id }}
        </template>
      </el-table-column>

      <el-table-column
        prop="code"
        label="客户编码"
        width="120"/>

      <el-table-column
        prop="company"
        label="公司名称"
        width="120"/>

      <el-table-column
        prop="contacts"
        label="联系人"
        width="120"/>

      <el-table-column
        prop="depot"
        label="分配仓库"
        width="120"/>

      <el-table-column
        prop="available"
        label="可用额度"
        width="120"/>

      <el-table-column
        prop="credit"
        label="信用额度"
        width="120"/>

      <el-table-column
        prop="currency"
        label="结算币种"
        width="120"/>

      <el-table-column
        prop="status"
        label="状态"
        width="120"/>
    </el-table>
  </div>
</template>

<script>
import { getList } from '@/api/table'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: null,
      listLoading: true,
      tableMultipleSelection: [],
      q_keyword: '',
      q_available: '',
      q_credit: '',
      p_create: '',
      q_status: '',
      q_status_options: [
        {
          value: 'pendingApproval',
          label: '待审核'
        }, {
          value: 'approve',
          label: '通过'
        }, {
          value: 'reject',
          label: '拒绝'
        }, {
          value: 'blockUp',
          label: '停用'
        }
      ],
      pickerOptions: {
        shortcuts: [{
          text: '最近一周',
          onClick(picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近一个月',
          onClick(picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近三个月',
          onClick(picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)
            picker.$emit('pick', [start, end])
          }
        }]
      }
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.listLoading = true
      getList(this.listQuery).then(response => {
        console.log(response.data.items)
        this.list = response.data.items
        this.listLoading = false
      })
    },
    handleSelectionChange(val) {
      this.tableMultipleSelection = val
    }
  }
}
</script>

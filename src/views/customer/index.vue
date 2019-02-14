<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      ref="multipleTable"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row
      @selection-change="handleSelectionChange">
      <el-table-column type="selection" width="55">
      </el-table-column>
      <el-table-column align="center" label="ID" width="95">
        <template slot-scope="scope">
          {{ scope.$id }}
        </template>
      </el-table-column>

      <el-table-column
        prop="code"
        label="客户编码"
        width="120">
      </el-table-column>

      <el-table-column
        prop="company"
        label="公司名称"
        width="120">
      </el-table-column>

      <el-table-column
        prop="contacts"
        label="联系人"
        width="120">
      </el-table-column>

      <el-table-column
        prop="depot"
        label="分配仓库"
        width="120">
      </el-table-column>

      <el-table-column
        prop="available"
        label="可用额度"
        width="120">
      </el-table-column>

      <el-table-column
        prop="credit"
        label="信用额度"
        width="120">
      </el-table-column>

      <el-table-column
        prop="currency"
        label="结算币种"
        width="120">
      </el-table-column>

      <el-table-column
        prop="status"
        label="状态"
        width="120">
      </el-table-column>
    </el-table>
    <div style="margin-top: 20px">
      <el-button @click="toggleSelection([tableData3[1], tableData3[2]])">切换第二、第三行的选中状态</el-button>
      <el-button @click="toggleSelection()">取消选择</el-button>
    </div>
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
      listLoading: true
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
    }
  }
}
</script>

<template>
<el-container class="codelabs-container">
  <el-main>
    <codelabs-list :list="codelabs" v-loading="isLoadingCodelabsList" element-loading-background="#fff"></codelabs-list>
  </el-main>
  <el-aside width="280px">
    <el-main>
      <el-button type="primary" @click="showCreateDialog">新建文档</el-button>
    </el-main>
  </el-aside>
  <codelabs-create-dialog></codelabs-create-dialog>
</el-container>
</template>

<script>
import CodelabsToolbar from '@/components/codelabs/CodelabsToolbar'
import NodeChooser from '@/components/forum/NodeChooser'
import CodelabsList from '@/components/codelabs/CodelabsList'
import CodelabsCreateDialog from '@/components/codelabs/CodelabsCreateDialog'
import { mapGetters } from 'vuex'
export default {
  name: 'codelabs',
  components: {
    CodelabsToolbar,
    NodeChooser,
    CodelabsList,
    CodelabsCreateDialog
  },
  computed: {
    ...mapGetters({
      codelabs: 'codelabs/codelabs',
      isLoadingCodelabsList: 'codelabs/isLoadingCodelabsList'
    }),
    isCreateDialogVisible: {
      get: function () {
        return this.$store.state.codelabs.isCreateDialogVisible
      },
      set: function (newValue) {
        return this.$store.dispatch('codelabs/setIsCreateDialogVisible', { isCreateDialogVisible: newValue })
      }
    }
  },
  methods: {
    showCreateDialog: function () {
      this.isCreateDialogVisible = true
    }
  },
  created () {
    this.$store.dispatch('codelabs/getCodelabs', { paginate: true, page: 1 })
  }
}
</script>

<style lang="scss">
.codelabs-container {
  margin: 80px auto 0;
  width: 1000px;
}
</style>


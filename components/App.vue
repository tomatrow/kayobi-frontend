<template>
    <div class="container">
        <div v-for="data in this.tableData">
            <Table v-bind:data="data"></Table>
        </div>
    </div>
</template>

<script>
import Vue from "vue"
import Table from "./Table.vue"
import api from "../scripts/api.js"

export default Vue.extend({
    data() {
        return {
            tableData: []
        }
    },
    mounted() {
        api.get("tabledata").then(res => (this.tableData = res.data.response))
    }
})
</script>

<style lang="less" scoped>
.container {
}
</style>

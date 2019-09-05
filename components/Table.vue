<template>
    <!-- <details class="container">
        <summary>{{ this.data.name }}</summary>
        <div v-for="item in this.items">
            <Row v-bind:data="item" v-bind:indexes="indexes"></Row>
        </div>
    </details> -->
    <div>
        <div>{{ this.data.name }}</div>
        <table>
            <thead>
              <tr>
                <th v-for="key in Object.keys(this.items[0])">
                  {{ key | capitalize }}
                </th>
              </tr>
            </thead>
            <tbody v-for="item in this.items">
                    <Row v-bind:data="item" v-bind:indexes="indexes"></Row>

            </tbody>
        </table>
    </div>

</template>

<script>
import Vue from "vue"
import api from "../scripts/api.js"
import Row from "./Row.vue"

export default Vue.component("Table", {
    props: ["data"],
    data() {
        return { items: [] }
    },
    mounted() {
        api.get(this.data.name).then(res => {
            this.items = res.data.response
            console.log(this.items)
        })
    },
    components: { Row },
    computed: {
        indexes: function() {
            return this.data.indexes.map(index => index.name)
        }
    }
})
</script>

<style lang="less" scoped></style>

<template>
    <!-- <details class="container" v-on:toggle="onToggle" ref="details">
        <summary
            >{{ this.data[this.indexes[0]] }}
            <button @click="save">Save</button></summary
        >
        <dl v-for="key in Object.keys(data)">
            <dt>{{ key }}</dt>
            <dd contenteditable="true" @input="dataChange">{{ data[key] }}</dd>
        </dl>
    </details> -->
    <tr>
        <td v-for="key in Object.keys(data)">
            {{ data[key] }}
        </td>
    </tr>

</template>

<script>
import Vue from "vue"
import api from "../scripts/api.js"

export default Vue.component("Row", {
    props: ["data", "indexes"],
    methods: {
        onToggle: function(event) {},
        save: function() {
            // get the current object state
            const details = this.$refs.details
            const keys = Array.from(details.querySelectorAll("dt")).map(
                x => x.innerText
            )
            const values = Array.from(details.querySelectorAll("dd")).map(
                x => x.innerText
            )
            const row = {}
            keys.forEach((key, index) => row[key] = values[index])

            api.post('/productlines',{
                keyName: this.$props.indexes[0],
                row
            })
        },
        dataChange(event) {
            console.log("Data change", event)
        }
    }
})
</script>

<style lang="less" scoped>
.container {
    margin-left: 20px;
}
</style>

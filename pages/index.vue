<template lang="pug">
    v-container(fluid)
        v-container
            v-row(justify="center")
                v-col(cols="6")
                    v-row
                        v-col(cols="8" class="headline") Properties
                        v-col(cols="4" class="headline") Order

                    Row(
                        v-for="(item, index) in rows"
                        :key="index"
                        :item="item"
                        :index="index"
                        @remove="removeRow(index)")

                    v-row(class="mb-3")
                        v-col(
                            cols="8"
                            class="d-flex justify-center")
                            v-btn(
                                @click="addRow"
                                class="mx-2"
                                color="success"
                                outlined
                                ) Add property
                            v-btn(
                                @click="sendData"
                                class="mx-2"
                                outlined
                                color="info"
                                :disabled="rows.length === 0"
                                ) Sort

            v-row(
                v-if="rows.length !== 0"
                justify="center")
                v-col(cols="8")
                    div(v-for="(row, index) of rows") {{ index + 1 }}. {{ row }}
</template>

<script>
    import Row from '~/components/Row'

    export default {
        name: 'main-page',
        components: { Row },
        computed: {
            rows: {
                get() {
                    return this.$store.state.rows
                },
                set(newVal) {
                    return this.$store.commit('setRows', newVal)
                }
            },
        },
        watch: {
            rows(){
                this.setPriority()
            }
        },
        methods: {
            addRow() {
                this.rows.push({
                    name: '',
                    title: '',
                    orderTypeDefault: '',
                    priority: ''
                })
            },
            removeRow(index) {
                this.rows.splice(index, 1);
            },
            setPriority(){
                this.rows.forEach((item, index) => item.priority = (index + 1));
            },
            sendData() {
                const data = JSON.stringify(this.rows);
                console.log(data);
            }
        }
    }
</script>

<style>

</style>


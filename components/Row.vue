<template lang="pug">
    v-row(
        justify="center"
        align="center")
        v-col(
            cols="8"
            class="d-flex align-center")
            div(class="mr-2 align-center") {{ index + 1 }}.

            v-select(
                v-model="rows[index]"
                :items="filteredFields"
                class="mr-2"
                item-text="title"
                item-value="name"
                item-disabled="disabled"
                label="select"
                return-object)

        v-col(cols="4")
            v-btn(
                @click="toggleOrder"
                outlined
                small
                fab
                color="info")
                span(v-if="rows[index].orderTypeDefault.length === 0")
                    v-icon mdi-sort
                span(v-else) {{ rows[index].orderTypeDefault }}

            v-btn(
                @click="remove"
                class="ml-2"
                outlined
                small
                fab
                color="error")
                v-icon(dark) mdi-close
</template>

<script>
    import _ from 'lodash'
    import { mapGetters } from 'vuex'

    export default {
        name: "Row-component",
        props: {
            index: Number
        },
        computed: {
            ...mapGetters(['fields']),
            rows: {
                get() {
                    return this.$store.state.rows
                },
                set(newVal) {
                    return this.$store.commit('setRows', newVal)
                }
            },
            filteredFields() {
                let filtered = _.difference(this.fields, this.rows);

                if (this.rows[this.index].name.length > 0) {
                    filtered.unshift(this.rows[this.index]);
                    return filtered;
                } else {
                    return filtered;
                }
            }
        },
        methods: {
            remove() {
                this.$emit('remove');
            },
            toggleOrder() {
                if (this.rows[this.index].orderTypeDefault.length === 0) return;

                const order = this.rows[this.index].orderTypeDefault;
                switch (order) {
                    case 'ASC':
                        this.rows[this.index].orderTypeDefault = 'DESC';
                        break;
                    case 'DESC':
                        this.rows[this.index].orderTypeDefault = 'ASC';
                        break;
                }
            }
        }
    }
</script>

<style scoped>

</style>

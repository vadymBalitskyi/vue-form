<template lang="pug">
  v-row(
    justify="center"
    align="center")
    v-col(
      cols="8"
      class="d-flex align-center")
      div(class="mr-2 align-center") {{ index + 1 }}.
      v-select(
        v-model="item.selected"
        :items="fields"
        @change="selectField($event, index)"
        class="mr-2"
        item-text="title"
        item-value="name"
        item-disabled="disabled"
        label="select"
        return-object)

    v-col(cols="4")
      v-btn(
        @click="toggleOrder(item)"
        outlined
        small
        fab
        color="info"
        )
        v-icon mdi-sort
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
  export default {
    name: "Row-component",
    props: {
      fields: Array,
      item: Object,
      index: Number
    },
    methods: {
      remove() {
        this.$emit('remove');
      },
      toggleOrder() {
        if(this.item['selected'].orderTypeDefault === 'ASC') {
          this.item['selected'].orderTypeDefault = 'DESC'
        } else {
          this.item['selected'].orderTypeDefault = 'ASC'
        }
      },
      selectField(item) {
        item['disabled'] = !item['disabled']
        console.log(item)
      }
    }
  }
</script>

<style scoped>

</style>

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
            :fields="fields"
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
                :disabled="fields.length === rows.length"
                ) Add property
              v-btn(
                @click="sendData"
                class="mx-2"
                outlined
                color="info"
                :disabled="rows.length === 0"
                ) Sort

          v-row(v-if="rows.length !== 0")
            v-col
              div Click "Sort": {{result}}
</template>

<script>
    import { mapGetters } from 'vuex'
    import Row            from '@/components/Row'

    export default {
      name: 'main-page',
      data: () => ({
        rows: [],
        result: []
      }),
      components: { Row },
      computed: {
        ...mapGetters(['fields'])
      },
      methods: {
        addRow() {
          const obj = {
            name: '',
            title: '',
            orderTypeDefault: '',
            priority: ''
          };
          this.rows.push(obj)
        },
        removeRow(index) {
          this.rows.splice(index,1);
        },
        sendData() {
          //deep copy
          let data = JSON.parse(JSON.stringify(this.rows));
          data.forEach((item, index) => {
            if('selected' in item) {
              data[index] = item['selected'];
            }
            data[index]['priority'] = index;
          });
          this.result = data;
          console.log('result', this.result)
        }
      }
  }
</script>

<style>

</style>


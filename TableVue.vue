<template>
  <section>
    <table class="table">
      <thead>
        <tr>
          <th v-for="column in tableColumns" :key="column.id">{{column.name}}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="index">
          <th v-for="(i ,configIndex) in tableCellConfig" :key="configIndex">
            <slot name="beforeCellContent" :itemIndex="index" :atribute="i.atributeToShow"></slot>
            <span v-if="i.url">
              <span class="component">
                <keep-alive>
                  <component :is="getComponent(i.url)" v-bind="i.atributos" :value="item[i.atributeToShow]"></component>
                </keep-alive>
              </span>
            </span>
            <slot name="cell" :itemIndex="index" :atribute="i.atributeToShow" :value="item[i.atributeToShow]" v-else>
              {{ item[i.atributeToShow] }}
            </slot>
            <slot name="afterCellContent" :itemIndex="index" :atribute="i.atributeToShow"></slot>
          </th>
          <th>
            <slot name="lastColumn" :itemIndex="index" :id="item.id"></slot>
          </th>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
export default {
  name: 'TableVue',
  props: {
    tableColumns: {
      type: Array,
      default: () => {},
    },
    tableCellConfig: {
      type: Array,
      default: () => {},
    },
    items: {
      type: Array,
      default: () => {},
    },
  },
  components: {

  },
  data: () => {
    return {};
  },
  computed: {
    getComponent() {
      return (url) => require(`${url}`).default;
    },
  },
}
</script>
<style scoped>
.component{
  display: inline-block;
}
</style>
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
            <slot name="beforeCellContent" :itemIndex="index" :attribute="i.attrToShow"></slot>
            <span v-if="i.path">
              <span class="component">
                <keep-alive>
                  <component :is="getComponent(i.path)" v-bind="i.atributos" :value="item[i.attrToShow]"></component>
                </keep-alive>
              </span>
            </span>
            <slot name="cell" :itemIndex="index" :attribute="i.attrToShow" :value="item[i.attrToShow]" v-else>
              {{ item[i.attrToShow] }}
            </slot>
            <slot name="afterCellContent" :itemIndex="index" :attribute="i.attrToShow"></slot>
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
      return (path) => require(`${path}`).default;
    },
  },
}
</script>
<style scoped>
.component{
  display: inline-block;
}
</style>
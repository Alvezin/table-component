<template>
  <section>
    <table class="table">
      <thead>
        <tr>
          <th v-for="(column, index) in tableColumns" :key="index">{{column}}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="index">
          <th v-for="(i ,configIndex) in tableCellConfig" :key="configIndex">
            <slot name="beforeCellContent" :itemIndex="index" :attribute="i.attrToShow"></slot>
            <slot v-if="i.path" name="cellComponent" :value="resolve(i.attrToShow, item)" :attrs="i.atributos" :itemIndex="index" :attribute="i.attrToShow">
              <span class="component">
                <keep-alive>
                  <component :is="getComponent(i.path)" v-bind="i.atributos" :value="resolve(i.attrToShow, item)"></component>
                </keep-alive>
              </span>
            </slot>
            <slot name="cell" :itemIndex="index" :attribute="i.attrToShow" :value="resolve(i.attrToShow, item)" v-else>
              {{ resolve(i.attrToShow, item) }}
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
  methods: {
    resolve(path, obj) {
      return path.split(".").reduce(function(prev, curr) {
        return prev ? prev[curr] : null
      }, obj || self)
    }
  },
}
</script>
<style scoped>
.component{
  display: inline-block;
}
</style>

<template>
  <div id="app">
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
    <TotalBalance :total="totalBalance"/>
    <Form @submitForm="onSubmit"/>
  </div>
</template>

<script>
import BudgetList from './components/BudgetList.vue';
import TotalBalance from './components/TotalBalance.vue';
import Form from './components/Form.vue';

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Part of salary',
        id: 1
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Penalty',
        id: 2
      },
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0);
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onSubmit(formName) {
      const newObj = {
        ...formName,
        id: String(Math.floor((Math.random() + 1) * 100))
      };

      this.$set(this.list, newObj.id, newObj);
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

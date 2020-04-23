<template>
    <div>
    <CRUE v-bind:tableData="tableData" v-bind:titleList="titleList" :w="width"></CRUE>
    </div>
</template>

<script>
import CRUE from './components/Crud'
export default {
    props: {

    },
    data() {
        return {
tableData:[
  {
          date: '2016-05-02',
          name: '王小虎1',
          address: '上海市普陀区金沙江路 1518 弄',
          name11: '王小虎4',
        }, {
          date: '2016-05-04',
          name: '王小虎2',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎3',
          address: '上海市普陀区金沙江路 1518 弄',
        }, {
          date: '2016-05-03',
          name: '王小虎4',
          name1: '王小虎4',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎4',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎4',
          address: '上海市普陀区金沙江路 1518 弄'
        }
],
titleList:["日期","姓名","地址","111"],
width:[100,200,300,400]
        };
    },
    computed: {

    },
    created() {

    },
    mounted() {

    },
    watch: {

    },
    methods: {

    },
    components: {
CRUE
    },
};
</script>

<style >

</style>

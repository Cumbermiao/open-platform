<template>
    <div>
        <Sheader :path='path' :title="title" :operation="operation"></Sheader>
        <v-content>
            <m-form :dataSource='dataSource' :opObj='opObj' @save='modify' :readonly='readonly'></m-form>
        </v-content>
    </div>
</template>

<script>
import Sheader from '../../components/SSheader'
import form1 from '../../components/form1'
import Content from '../../components/Content'
import axios from '../../utils/axios';
import { mapActions, mapState, mapMutations } from 'vuex';


export default {
    data() {
        return {
            title: '数据源管理',
            operation: '>查看',
            dataSource:[],
            readonly:true,
            path:'/'
        }
    },
    computed:{
        ...mapState({
            opObj:state=>state.home.opObj,
            pageNum: state => state.home.pageNum,
            totalSize: state => state.home.totalSize,
            keywords: state => state.home.keywords,
            pageSize: state => state.home.pageSize,
            currentId: state => state.home.currentId,
            dataSourceWid: state => state.home.dataSourceWid,
            catalogWid: state => state.home.currentId,
            inParams: state => state.home.inParams,
            outParams: state => state.home.outParams,
        })
    },
    components: {
        vContent: Content,
        mForm: form1,
        Sheader,
    },
    methods:{
        modify(val){
            this.$store.commit('modify',val)
        }
    },
    mounted() {
        console.log('xxx')
        axios.post('/metadata/datasource/selectList').then((res) => { 
            this.dataSource=res.data.dataSet 
            console.log(this.dataSource)
            })
        .catch((err) => { console.log(err) })
    }
}
</script>

<style scoped>

</style>


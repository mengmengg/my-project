<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2 id="ss">Essential Links</h2>

    <el-button type="text" @click="open">点击打开 Message Box</el-button>
    <el-button type="text" @click="outerVisible = true">点击打开外层 Dialog</el-button>
    <router-link to="/cardInfo" >demo1</router-link>
    <el-dialog title="外层 Dialog" :visible.sync="outerVisible" :close-on-click-modal="innerVisible">
      <el-dialog
        width="30%"
        title="内层 Dialog"
        :visible.sync="innerVisible"
        append-to-body>
      </el-dialog>
      <card-item></card-item>
      <div slot="footer" class="dialog-footer">
        <el-button @click="outerVisible = false">取 消</el-button>
        <el-button type="primary" @click="innerVisible = true">打开内层 Dialog</el-button>
      </div>
    </el-dialog>

  </div>
</template>

<script>
  import cardItem from  '@/components/cardItem'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      a:false,
      outerVisible: false,
      innerVisible: false
    }

  },
  created(){

    this.$axios.get('https://geo.datav.aliyun.com/areas/bound/geojson?code=100000').then(function(res){
      console.log(res)
    }).catch(function (error) {
      console.log(error);
    });
  },

  components:{
    cardItem
  },
  methods:{
    changeMask(item){
      item.currentTarget
    },
    but(){
      this.add=true;
    },
    open() {
      var html='233443433443'
      var then=this;
      this.a=true;
       // then.$alert(html, 'HTML 片段', {
       //     dangerouslyUseHTMLString: true,
       //     showConfirmButton:false
       // });

    },
    getdata(){
      /*axios({
          method: 'post',
          url: '/user/12345',
          data: {
              firstName: 'Fred',
              lastName: 'Flintstone'
          }

      });*/
    }

  },mounted(){
    alert($("#ss").text())
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;

}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

<template>
    <div class="wrapper-content wrapper-content--fixed">
      <section>
        <div class="container">
<!-- wrapper -->
          <div class="notify__wrapper">

            <!-- title -->
            <div class="notify-title">
              <p>Notify App</p>
              <!-- svg -->
              <svg></svg>
            </div>

            <!-- notify -->
            <div class="notify__content">
              <notify
              :messages = "messages"/>
            </div>

          </div>
        </div> 
      </section>
    </div>  
</template>


<script>
import axios from 'axios'
import notify from '@/components/Notify.vue'
export default {
  components : {notify},
  data () {
    return {
      messages : []
    }
  },
  mounted () {
    this.getNotify()
  },
  methods : {
    getNotify () {
      this.loading = true
      axios
    .get('https://tocode.ru/static/c/vue-pro/notifyApi.php')
    .then(response => {
      let res = response.data.notify
      this.messages = res
    })
    .catch(error =>{
      console.log(error)
    })
    .finally( () =>(this.loading = false))
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 90vh;
}
.notify__wrapper {
  width: 400px;
  background-color: #fff;
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 12px 22px 0 rgba(0,0,0,.1); 
}
.notify__content{
  display: flex;
  align-items: center;
  flex-direction: column;
  min-height: 300px;
}
.notify-title{
  display: flex;
  align-items: center;
  justify-content: space-between;
  p{
    font-size: 24px;
  }

}
</style>
<script>
import Vue from 'vue';
import PetraVue from '@/petra-vue.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    PetraVue,
  },
  data() {
    return {
      data:{
        amount: 100000,
        title : 'Pay with Petra',
        email: 'emmanueltolu.adebayo@gmail.com',
        key:'pk_test_U4GzNZdtkqC0Oxkdi4FkmH9JLNcE1DKe',
        id:"8a24eb20-5721-4183-987d-aa6bc371ab60",
        payType: "p",
        reference: "",
        button : {
          backgroundColor: "#f7a200",
          border: "none",
          borderRadius: "8px",
          color: "white",
          textAlign: "center",
          textDecoration: "none",
          height: "50px",
          width: "250px",
          display: "inline-flex",
          alignItems: 'center',
          justifyContent: 'center',
          fontSize: "16px",
          transitionDuration: "0.4s",
          cursor: "pointer",
          padding: "10px 32px",
          opacity: "1"
        }
      }
    }
  },

  methods: {
    onClose(){
      alert('Payment modal closed')
    },
    onSuccess: ()=>{
      // alert('')
    }
  },
});
</script>

<template>
  <div id="app">
    <petra-vue       :data="data"
                     :onClose="onClose"
                     :onSuccess="onSuccess" />

  </div>
</template>

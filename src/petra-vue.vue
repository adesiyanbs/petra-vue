<script>

export default /*#__PURE__*/{
  name: 'PetraVue', // vue component name
  props: ['data', 'onSuccess', 'onClose'],
  data() {
    return {
      myModal:{display: "none"},
      dbutton2: {
        backgroundColor: "#F7A200",
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
        fontSize: "14px",
        transitionDuration: "0.4s",
        cursor: "pointer",
        padding: "10px 32px",
        opacity: "1",
      },
      dModalContent :{
        backgroundColor: "#fefefe",
        margin: "auto",
        padding: "10px",
        width: "80%",
        height: "80%",
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        borderRadius:"5px",
      },
      dIframe :{
        display: "none",
        border: "none",
        height: "100%",
        width: "100%",
        marginTop:"20px",
        zIndex: "99999",
      },
      dModalClose :{
        color: "#aaaaaa",
        position: "absolute",
        top: "2%",
        right: "10%",
        float: "right",
        fontSize: "28px",
        fontWeight: "bold",
        cursor: "pointer",
        zIndex: "100000",
      },
      dModal:{
        display: "none",
        position: "fixed",
        zIndex: "1",
        paddingTop: "20px",
        left: "0",
        top: "0",
        width: "100%",
        height: "100%",
        overflow: "auto",
        
        // backgroundColor: "rgb(0,0,0)",
        backgroundColor: "rgba(0,0,0,0.4)",
      },
      loaderWrapper: {
        height: "100vh",
        display: "grid",
        placeItems: "center",
      },
      loaderImg: {
        height: "100px",
        width: "100px",
        display: "block",
        animation: "loader 1s 1s infinite",
      }
    }
  },
  methods: {
    mover(){
      this.dbutton2.opacity = "0.8"
    },

    moout() {
      this.dbutton2.opacity = "1"
    },

    openIframe() {
      this.handleAnimation();
      this.dModal.display = 'block'
     // this.$refs.dFrame.addEventListener('load', this.handleIframeLoaded, true)
      this.iframeData(this)
    },

    handleIframeLoaded() {
   //   this.$refs.dFrame.removeEventListener('load', this.handleIframeLoaded, true)
      this.$refs.loaderImg.style.display = "none";
      this.$refs.dFrame.style.display = "block";
      console.log('HANDLE LOAD')
    },

    closeModal(data){
      if(data) data()
      // eslint-disable-next-line no-self-assign
      this.$refs.dFrame.src = this.$refs.dFrame.src
      this.dModal.display = 'none'
    },

    handleAnimation() {
      this.$refs.dFrame.style.display = 'none'
      const loader = this.$refs.loaderImg;
      if (!loader) {
        loader.setAttribute('src', 'https://www.thepetra.co/favicon.ico')
      }
      loader.style.display = 'block'
      loader.animate([
        // keyframes
        { transform: 'scale(0.7)' },
        { transform: 'scale(0.8)' },
        { transform: 'scale(0.7)' }
      ], {
        // timing options
        duration: 1000,
        iterations: Infinity
      });
      setTimeout(() => {
        this.$refs.loaderImg.style.display = "none";
        this.$refs.dFrame.style.display = "block";
      }, 7000);
    },

    iframeData(dataFunc){
      window.addEventListener('message', function(event) {
        if (event.origin == 'https://www.thepetra.co/'){
          if(event.data == 'false pass'){
            dataFunc.closeModal(dataFunc.onClose)

          }
          if(event.data == 'false pass1'){
            dataFunc.closeModal(dataFunc.onSuccess)
          }
        }
      })
    },
  },
};
</script>

<template>
  <div>
    <button
        v-html="`${data.title}`"
        :style="data.button"
        @mouseover="mover()"
        @mouseleave="moout()"
        @click="openIframe()"
    >

    </button>
    <br><br>

    <div :style="dModal">
      <div :style="dModalContent">
        <div ref="loaderWrapper" id="loaderWrapper" :style="loaderWrapper">
          <img ref="loaderImg" alt="loader" :style="loaderImg" id="loaderImg" src="https://www.thepetra.co/favicon.ico" />
        </div>
        <span class="close" :style="dModalClose" @click="closeModal()"><img src="../assets/close.svg" alt=""></span>
        <iframe
            ref="dFrame"
            :src="`https://checkout.petra.africa/?amount=${data.amount}&email=${data.email}&key=${data.key}&payType=${data.payType ? data.payType + '&id='+data.id : ''}`"
            frameborder="0"
            :style="dIframe"
        ></iframe>
      </div>
    </div>

  </div>
</template>

<style scoped>
  .petra-vue {
    display: block;
    width: 400px;
    margin: 25px auto;
    border: 1px solid #ccc;
    background: #eaeaea;
    text-align: center;
    padding: 25px;
  }
  .petra-vue p {
    margin: 0 0 1em;
  }
  
</style>

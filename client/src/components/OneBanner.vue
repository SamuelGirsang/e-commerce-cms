<template>
  <div class="container">
    <div class="form-box">
      <div class="left">
        <img :src="$store.state.oneProduct.image_url"
         style="height: 19rem; width: 19rem;" alt="">
        <!-- <p>Title: {{ $store.state.oneProduct.name }}</p> -->
        <div class="price-stock-box">
        <!-- <p>Price: {{ $store.state.oneProduct.price }}</p>
        <p>Stock: {{ $store.state.oneProduct.stock }}</p> -->
        </div>
      </div>
        <!-- <h1>{{ oneProduct.name }}</h1> -->
        <!-- <h1>halo</h1> -->
      <div class="right">
      <form @submit.prevent="updateBanner">
        <h2>{{ $store.state.oneProduct.title }}</h2>
        <input type="text" class="field" v-model="input.title"
          name="" id=""
          placeholder="Update banner title"
        >
        <input type="text" class="field" v-model="input.image_url" name=""
          id=""
          placeholder="Update the image url banner"
        />

        <p>Is banner has a promo? </p>

          <label id="radio1" class="radio-inline">
            <input type="radio"  class="field" value="true" v-model="input.status" name=""
              required
            > Yes
          </label>
          <label id="radio2" class="radio-inline">
            <input type="radio" class="field" value="false" v-model="input.status" name=""
              required
          > No
          </label>
        <div class="btn-wrapper">
          <button id="btn1" class="btn">Update</button>
        </div>
      </form>
          <button @click.prevent="deleteBanner" id="btn2" class="btn">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OneBanner',
  // props: ['product'],
  data () {
    return {
      input: {
        title: '',
        status: '',
        image_url: ''
      }
    }
  },
  methods: {
    getOneBanner () {
      const bannerId = this.$route.params.banner_id
      this.$store.dispatch('getOneBanner', bannerId)
      // this.imageUrl = this.$store.state.product.oneProduct.image_url
    },
    updateBanner () {
      const dataBanner = {
        title: this.input.title,
        status: this.input.status,
        image_url: this.input.image_url,
        id: this.$route.params.banner_id
      }
      this.$store.dispatch('updateBanner', dataBanner)
    },
    deleteBanner () {
      console.log('ONEPRO')
      const deleteId = this.$route.params.banner_id
      this.$store.dispatch('deleteBanner', deleteId)
    }
  },

  // computed: {
  //   oneProduct () {
  //     return this.$store.state.oneProduct
  //   }
  // },
  mounted () {
    this.getOneBanner()
  }
}
</script>

<style scoped>
.container {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px 100px;
  font-family: Clarkson;
}
.container:after {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  /* background: url() no-repeat center; */
  filter: blur(50px);
  z-index: -1;
}

.form-box {
  max-width: 850px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #fff;
  box-shadow: 0 0 19px 5px rgba(0,0,0,0.19);
}

.left {
  /* background: url('../assets/sf-wp5.jpg')no-repeat center; */
  background-size: cover;
  height: 90%;
  margin: 10px;
  padding: 25px 40px;
}

.price-stock-box {
  margin: 10px 0 0 0px;
}

.left p {
  margin: 7px 0 0 0;
}

.right {
  padding: 25px 40px;
}

h2 {
  position: relative;
  padding: 0 0 10px;
  margin-bottom: 10px;
}

h2:after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translateX(-50%);
  height: 4px;
  width: 50px;
  border-radius: 2px;
  background-color: #2ecc71;
}

.field {
  width: 100%;
  border: 2px solid rgba(0,0,0,0);
  outline: none;
  background-color: rgba(230, 230, 230, 0.6);
  padding: 0.5rem 1rem;
  font-size: 1.1rem;
  margin-bottom: 22px;
  transition: .3s;
}

.field:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

textarea {
  min-height: 150px;
}

#radio1 {
  margin: 10px 30px 0 0;
  /* margin: 5px; */
}

#radio2 {
  margin: 0 0 10px 30px;
  /* margin: 5px; */
}

.btn {
  margin: 10px 0 0 0;
}

/* .btn-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
} */
  /* justify-content: space-between; */

#btn1 {
  width: 30%;
  padding: 0.4rem 0.5rem;
  background-color: #2ecc71;
  color: #fff;
  font-size: 0.9rem;
  border: #fff;
  outline: none;
  cursor: pointer;
  transition: .3s;
}

#btn1:hover {
  background-color: #27ae60;
}

#btn2 {
  width: 30%;
  padding: 0.4rem 0.5rem;
  background-color: #cc402e;
  color: #fff;
  font-size: 0.9rem;
  border: #fff;
  outline: none;
  cursor: pointer;
  transition: .3s;
  margin: 10px;
}

#btn2:hover {
  background-color: #ae3b27;
}

.field:focus {
  border: 2px solid rgba(30,85,250,0.47);
  background: #fff;
}

@media screen and (max-width: 880px) {
  .form-box {
    grid-template-columns: 1fr;
  }
  .left {
    height: 200px;
  }
}
</style>

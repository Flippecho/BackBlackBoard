<template>
  <div class="youth-study">
    <div class="youth-study-info">
      <div id="youth-study-current" class="card">
        <div class="card-header">{{ current.episode }}</div>
        <img :src="current.imgUrl" class="card-img-top" alt="">
        <div class="card-body">
          <p class="card-title">{{ current.title }}</p>
        </div>
      </div>

      <div id="youth-study-history" class="carousel slide card" data-bs-touch="false" data-bs-interval="false">
        <div class="card-header">往期回顾</div>
        <div class="carousel-inner">
          <div class="carousel-item active">
            <img :src="previous.imgUrl" alt="">
            <div class="card-body">
              <p class="card-title">{{ previous.title }}</p>
            </div>
          </div>
          <div>
            <div class="carousel-item" v-for="(item, index) in history" :key="index">
              <img :src="item.imgUrl" alt="">
              <div class="card-body">
                <p class="card-title">{{ item.title }}</p>
              </div>
            </div>
          </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#youth-study-history" data-bs-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#youth-study-history" data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </div>
    <div class="youth-study-upload">
      <div class="input-group">
        <input type="file" class="form-control" id="inputGroupFile" aria-describedby="inputGroupFileAddon"
               aria-label="Upload" accept="image/*" @change="triggerFile($event)" ref="input">
        <button class="btn btn-secondary" type="button" id="inputGroupFileAddon">上传</button>
      </div>
      <img :src="imgUrl" alt=""/>
    </div>
  </div>
</template>

<script>
export default {
  name: "YouthStudy",
  data() {
    return {
      isSelectFile: false,
      imgUrl: require("../assets/截图样例.jpg"),
      current: {
        episode: '第十二季第十四期',
        imgUrl: 'https://pic.cyol.com/img/20220103/img_96014bc84db0c0d045fc5ad7a777cc9598b3.jpeg',
        title: '深化对新时代党的创新理论的理解和掌握'
      },
      previous: {
        imgUrl: 'https://pic.cyol.com/img/20211227/img_96013deb5b9d2a013f5b75b46bce969537bf.jpeg',
        title: '党百年奋斗的历史经验'
      },
      history: [
        {
          imgUrl: 'https://pic.cyol.com/img/20211220/img_9601e21b91a2a40b617becf6ea65ebba3e7a.jpeg',
          title: '党百年奋斗的重大成就和历史意义'
        },
        {
          imgUrl: 'https://pic.cyol.com/img/20211213/img_960198bc2d316dbe7f12dd7b0f31b5251d33.jpeg',
          title: '坚持和发展中国特色社会主义'
        },
        {
          imgUrl: 'https://pic.cyol.com/img/20211227/img_96013deb5b9d2a013f5b75b46bce969537bf.jpeg',
          title: '党百年奋斗的历史经验'
        }
      ]
    }
  },
  methods: {
    triggerFile: function (event) {
      let file = event.target.files[0];
      let url = "";
      const reader = new FileReader();
      reader.readAsDataURL(file);
      let that = this;
      reader.onload = function () {
        url = this.result.substring(this.result.indexOf(",") + 1);
        that.imgUrl = "data:image/png;base64," + url;
      };
    },
    openImg() {
      this.$refs.input.click();
    }
  }
}
</script>

<style scoped>

.youth-study {
  --third-study-x: calc((100vw - 9rem - 24rem - 347px) / 3);
  display: grid;
  grid-template-columns: calc(100vw - 9rem - 24rem - var(--third-study-x)) calc(24rem + var(--third-study-x));
}

.youth-study-info {
  height: 100vh;
  display: grid;
  grid-template-rows: 50vh 50vh;
}

#youth-study-current {
  margin: 3rem var(--third-study-x) auto var(--third-study-x);
}

#youth-study-history {
  margin: auto var(--third-study-x) 3rem var(--third-study-x);
}

.card {
  width: 347px;
  background: linear-gradient(145deg, #ffffff, #e6e6e6);
  box-shadow: 7px 7px 21px #d6d6d6,
  -7px -7px 21px #ffffff;
}

.card-header {
  font-size: 2rem;
  padding: 1rem;
}

.card-img-top {
  width: 345px;
  height: 194px;
  border-radius: 0;
}

.carousel {
  width: 347px;
}

.carousel-item > img {
  width: 345px;
  height: 194px;
}

.youth-study-upload {
  height: 100vh;
}

.youth-study-upload .input-group {
  width: 24rem;
  margin: 3rem var(--third-study-x) 0.3rem 0;
}

.youth-study-upload > img {
  width: 24rem;
  margin: 0 var(--third-study-x) auto 0;
  border-radius: 3px;
}


</style>
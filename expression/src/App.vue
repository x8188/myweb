<template>
  <div id="app">
    <div style="">
      <div id="nav" :style="opacityStyle">
        <div id="title">
          <span>DEEPCBA</span>
          <img
            src="./img/logo/logo.png"
            style="width: 70px; height: 70px"
          />
        </div>

        <router-link to="/">HOME</router-link> |
        <!-- <a-dropdown>
          <a class="ant-dropdown-link" @click="(e) => e.preventDefault()">
            TOOLS <a-icon type="down" />
          </a>
          <a-menu slot="overlay" @click="onClick" @visbleChange="visibleChange">
            <a-menu-item key="Methylation"> Methylation </a-menu-item>
            <a-menu-item key="Expression"> Expression </a-menu-item>
          </a-menu>
        </a-dropdown> -->
        <a-dropdown placement="bottomCenter">
          <a class="ant-dropdown-link">
            TOOLS<i class="el-icon-arrow-down el-icon--right"></i>
          </a>
          <a-menu slot="overlay" id="tool">
            <a-menu-item
              ><router-link to="/Expression/index"
                >Expression</router-link
              ></a-menu-item
            >
            <a-menu-item
              ><router-link to="/Methylation"
                >Methylation</router-link
              ></a-menu-item
            >
          </a-menu>
        </a-dropdown>
        <!-- <router-link to="/Expression">TOOLS</router-link> | -->
        <router-link to="/search">SEARCH</router-link> |
        <router-link to="/result">RESULT</router-link> |
        <router-link to="/about">CONTACT</router-link>
        <router-link to="/tutorial">TUTORIAL</router-link>

      </div>
      <section class="featured1"></section>
      <!-- <div id="welcome">

      </div> -->
      <div style="">
        <router-view />
      </div>
      <div class="foot">
        <h1
          style="
            color: white;
            font-weight: bold;
            font-size: 30px;
            text-align: center;
          "
        >
          Contact
        </h1>
        <p
          style="
            width: 50%;
            text-align: center;
            margin: 0 auto;
            padding: 10px 0;
          "
        >
          Address: Room B111, National Key Laboratory of Crop Genetic
          Improvement, Huazhong Agricultural university, Wuhan, 430070, China
          ?????????????????????????????????????????????????????????B111??? Tel: 027-87280350 Email:
          weibo.xie [at] mail.hzau.edu.cnt
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      backShow: false,
      opacityStyle: {
        opacity: 1, //????????????0??????
      },
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      //????????????start
      var scrollTop = document.documentElement.scrollTop;
      // console.log(scrollTop);
      if (scrollTop > 0) {
        let opacity = 0.3 + scrollTop / 210;
        let height = 100 - 40 * (scrollTop / 300);
        height = height < 60 ? 60 : height;
        // console.log("height", height);
        opacity = opacity > 1 ? 1 : opacity; //????????????0???1
        this.opacityStyle = {
          // opacity: opacity,
          height: height + "px",
          "line-height": height + "px",
        };
        this.backShow = true;
      } else {
        this.backShow = false;
      }
      //????????????end
    },
    onClick({ key }) {
      this.$router.push(`/tools/${key}`);
      console.log(this.$router);
      console.log(`Click on item ${key}`);
    },
    visibleChange(visible) {
      console.log(visible);
    },
  },
};
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 1000px;
  margin: 0 auto;
}
#title {
  position: absolute;
  left: 20px;
  font-size: 30px;
  color: #fff;
}
/* #welcome{
  width: 100%;
  background-image:url('../dist/img/welcome.jpg');
} */
#nav {
  line-height: 100px;
  /* background-color: rgb(0, 0, 0); */
  background-image: url("./img/back.png");

  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
  text-align: center;
  height: 100px;
  display: block;
  text-align: center;
  margin-bottom: 0;
  padding-bottom: 0;
}

#nav a {
  margin: 50px;
  font-weight: bold;
  font-size: 25px;
  color: #fff;
}
#tool a {
  /* Margin  : 10px; */
  height: 50px;
  font-weight: bold;
  font-size: 20px;
  color: #42b983;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
.foot {
  /* position: fixed; */
  bottom: 0px;
  background-color: black;
  color: white;
  height: 200px;
  /* text-align: center; */
  /* margin: 0 auto; */
}
section.featured1 {
  padding: 40px 0 60px;
  /* background: #70b9b0; */
  background-image: url("./img/back.png");
  color: #fdfdfd;
}
</style>

<template>
  <main>
    <!-- Top DropDown Section -->
    <section id="h-section">
      <DropCart :cartItems="cart" v-show="cartToggle" />
      <div id="orange-t" v-bind:style="{ backgroundImage: 'url(' + orangeBg + ')' }">
        <div id="header">
          <img id="logo" src="@/assets/images/logo.png" alt="Missing image." />
          <div id="nav">
            <span class="nav-bar">Features</span>
            <span class="nav-bar">Pricing</span>
            <span class="nav-bar" id="right-nav" @click="cartToggle = !cartToggle">Your Cart</span>

            <img
              id="cart-i"
              src="@/assets/images/cart.png"
              alt="Missing image."
              @click="cartToggle = !cartToggle"
            />
            <div id="cart-num-i">{{cart.length === 0 ? 0 : cart.length}}</div>
          </div>
        </div>
      </div>
      <div id="top-p">
        <div class="elevate">
          <span class="bolder">Elevate</span> Your Practice
          <span class="bolder">Effectively</span>
        </div>
        <div id="elevate-p">
          Add revenue to your practice. Utilize one platform and our technology to take your practice to the next level.
          <br />Simpatra has created marketing tools and packages that work for you while you care for your patients.
        </div>
      </div>
    </section>
    <!-- Middle Woman Section -->
    <section id="mid-section">
      <article id="mid-p">
        <div id="power">
          The Power
          <br />of the Directory
        </div>
        <div id="power-h-p">
          <span class="power-h">Traffice Source with Paid Advertising</span>
          <br />
          <p class="power-p">
            reperio bea et volorio dolenitia verrum quodit et, qua
            <br />Lum is maxim aceribus. Duci tem quo blaturi volor alitati
          </p>

          <br />
          <span class="power-h">Your Profile: Tell Them Who You Are!</span>
          <br />
          <p class="power-p">
            reperio bea et volorio dolenitia verrum quodit et, qua
            <br />Lum is maxim aceribus. Duci tem quo blaturi volor alitati
          </p>
          <br />
          <span class="power-h">Reach Out: Generate New Leads</span>
          <br />
          <p class="power-p">
            reperio bea et volorio dolenitia verrum quodit et, qua
            <br />Lum is maxim aceribus. Duci tem quo blaturi volor alitati
          </p>
        </div>
      </article>
      <img class="woman" src="@/assets/images/woman.jpeg" />
    </section>
    <!-- Video -->
    <section id="vid-products">
      <div id="vid-cont">
        <div id="computer" v-bind:style="{ backgroundImage: 'url(' + computer + ')' }">
          <iframe
            id="video"
            src="https://www.youtube.com/embed/BKorP55Aqvg"
            frameborder="0"
            allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>
      </div>
      <!-- Product Slider -->
      <ProductSelector :cartItems="cart" />
    </section>
    <!-- Footer Section -->
    <section id="f-section">
      <article id="bot-p">
        <div id="bot-cont">
          <div id="want">
            Want to Drive Traffic
            <br />to Your Practice
          </div>
          <div id="power-h-p">
            <span class="power-h">Generate Traffic</span>
            <br />
            <p class="power-p">
              reperio bea et volorio dolenitia verrum quodit et, qua
              <br />Lum is maxim aceribus. Duci tem quo blaturi volor alitati
            </p>

            <br />
            <span class="power-h">Utilize Our Bots</span>
            <br />
            <p class="power-p">
              reperio bea et volorio dolenitia verrum quodit et, qua
              <br />Lum is maxim aceribus. Duci tem quo blaturi volor alitati
            </p>
            <br />
            <span class="power-h">Audience Analytics</span>
            <br />
            <p class="power-p">
              reperio bea et volorio dolenitia verrum quodit et, qua
              <br />Lum is maxim aceribus. Duci tem quo blaturi volor alitati
            </p>
          </div>
        </div>
        <img id="drive" src="@/assets/images/DriveTraffic.png" />
      </article>
      <div id="orange-t-2" v-bind:style="{ backgroundImage: 'url(' + orangeBg + ')' }">
        <div id="bot-p">
          <div id="powerful" class="elevate">
            <span class="bolder">Powerful</span> Tools
            <br />that Work
            <span class="bolder">for You!</span>
          </div>
          <div id="join">JOIN TODAY AT $499 MONTHLY.</div>
          <button id="btn-getstrt">GET STARTED</button>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import orangeBg from "@/assets/images/OrangeBar.jpg";
import computer from "@/assets/images/Computer_Graphic.png";
import ProductSelector from "./ProductSelector.vue";
import DropCart from "./DropCart.vue";
export default {
  name: "Home",
  components: {
    ProductSelector,
    DropCart
  },
  data: () => {
    return {
      cart: [],
      orangeBg,
      computer,
      cartToggle: false
    };
  }
};
</script>

<style>
/*Container------------------------------------------------------------------------------*/
main {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: white;
}

.component-fade-enter-active,
.component-fade-leave-active {
  transition: opacity 0.3s ease;
}

.component-fade-enter,
.component-fade-leave-to {
  opacity: 0;
}

#orange-t {
  height: 1000px;
  -webkit-clip-path: polygon(0 0, 100% 0, 100% 56%, 0 100%);
  clip-path: polygon(0 0, 100% 0, 100% 60%, 0 100%);
  background-size: cover;
  background-position: center;
  z-index: -1;
}

/*Header------------------------------------------------------------------------------*/

#h-section {
  height: 1050px;
}
#header {
  display: flex;
  position: relative;
  background: transparent;
  height: 200px;
  margin: 0;
  width: 100%;
}
#nav {
  display: flex;
  position: absolute;
  margin-right: 130px;
  font-size: 20px;
  top: 100px;
  color: white;
  right: 0;
  height: 50px;
  width: 350px;
  justify-content: space-around;
  align-items: center;
}
.nav-bar:hover {
  cursor: pointer;
  text-decoration: underline;
}
#right-nav {
  margin-right: 20px;
}
#cart-num-i {
  position: absolute;
  right: 0;
  top: 0;
  width: 10px;
  height: 9px;
  padding-top: 1px;
  border-radius: 50%/50%;
  font-size: 7px;
  color: white;
  font-weight: 600;
  background-color: purple;
  border: solid white 1px;
  z-index: 2;
  margin-right: -16px;
  margin-top: 7px;
  text-align: center;
  vertical-align: middle;
  cursor: default;
}
#logo {
  height: 100px;
  position: absolute;
  top: 60px;
  left: 65px;
  width: 330px;
}
#cart-i {
  width: 30px;
  position: absolute;
  height: 30px;
  margin-left: 170px;
}
#cart-i:hover {
  transition: 0.2s;
  transform: scale(1.3);
  cursor: pointer;
}
/*Top Section------------------------------------------------------------------------------*/
#top-p {
  display: flex;
  flex-direction: column;
  width: 850px;
  height: 300px;
  margin: 100px 220px;
}
.elevate {
  color: white;
  font-size: 80px;
  margin-bottom: 40px;
}
.bolder {
  font-weight: 800;
}
#elevate-p {
  color: white;
  font-size: 30px;
  line-height: 35px;
  padding-left: 5px;
  line-height: 50px;
}
/*Woman Section------------------------------------------------------------------------------*/
#mid-section {
  display: flex;
  flex-direction: row;
  position: relative;
  height: 885px;
}
#mid-p {
  display: flex;
  flex-direction: column;
  width: 700px;
  margin-left: 220px;
  z-index: 1;
}
#power {
  font-size: 75px;
  color: rgba(65, 120, 151, 0.699);
  margin-bottom: 40px;
}
#power-h-p {
  line-height: 34px;
}
.power-h {
  font-size: 30px;
  font-weight: 600;
  color: rgba(0, 0, 0, 0.678);
}
.power-p {
  font-size: 23px;
  font-weight: lighter;
}
.woman {
  height: 1100px;
  width: 1700px;
  position: absolute;
  border-radius: 200px;
  z-index: 0;
  margin-left: 800px;
  margin-top: -215px;
  object-fit: fill;
}
/*Video------------------------------------------------------------------------------*/
#vid-products {
  background-color: rgba(128, 128, 128, 0.178);
  height: 1360px;
  padding: 0 200px;
}
#vid-cont {
  display: flex;
  justify-content: center;
  border-bottom: dotted 3px;
  height: 600px;
  position: relative;
}
#computer {
  height: 1100px;
  position: absolute;
  margin-bottom: 40px;
  bottom: 0;
  width: 1400px;
  background-size: cover;
  background-position: cover;
}
#video {
  position: absolute;
  width: 933px;
  height: 589px;
  margin-left: 235px;
  margin-bottom: 128px;
  bottom: 0;
  z-index: 1;
}
/* Lower Section ------------------------------------------------------------------------------*/
#bot-cont {
  display: flex;
  flex-direction: column;
  width: 700px;
  margin-left: 220px;
  z-index: 1;
}
#bot-p {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 700px;
  z-index: 1;
  margin-bottom: -250px;
}
#drive {
  height: 625px;
  width: 700px;
  margin-left: 1100px;
  margin-top: 70px;
  position: absolute;
  z-index: -2;
  object-fit: fill;
}
#want {
  font-size: 75px;
  width: 800px;
  color: rgba(65, 120, 151, 0.699);
  margin-top: 150px;
  margin-bottom: 40px;
}
#orange-t-2 {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 200px;
  text-align: center;
  height: 1100px;
  -webkit-clip-path: polygon(0 0, 100% 0, 100% 56%, 0 100%);
  clip-path: polygon(0 40%, 100% 0, 100% 100%, 0 100%);
  background-size: cover;
  background-position: center;
  z-index: -1;
}
#powerful {
  width: 800px;
}
#join {
  padding: 0 30px;
  font-size: 26px;
  color: white;
  font-weight: 600;
}
#btn-getstrt {
  margin: 50px auto;
  color: white;
  font-size: 26px;
  font-weight: 700;
  width: 435px;
  height: 105px;
  border-radius: 15px;
  border: none;
  background-color: rgba(119, 2, 119, 0.815);
}
#btn-getstrt:hover {
  background-color: rgba(211, 43, 211, 0.753);
  transition: 0.3s;
  transform: scale(1.1);
  cursor: pointer;
}
</style>
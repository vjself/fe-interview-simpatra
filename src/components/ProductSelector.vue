<template>
  <div id="product-s-cont" @mouseover="stopRotation()" @mouseleave="startRotation()">
    <div id="num-container">
      <div
        class="num"
        :style="product.id === currentNumber ? classA : classB"
        @click="carouselNav(product.id)"
        v-for="product in products"
        :key="product.id"
      >{{product.id}}</div>
    </div>
    <img id="btn-arrow-r" @click="next()" :src="arrow" />
    <img id="btn-arrow-l" @click="prev()" :src="arrowL" />
    <div id="img-cont">
      <img id="product-cont" :src="image" />
    </div>
    <div id="prod-dtls">
      <div id="sku">
        <span id="o-prod">BEST SELLER //</span>
        <span id="b-prod">&nbsp;{{sku}}</span>
        <br />
        <br />
        <div id="prod-name">
          <span id="o-prod">{{name}}</span>
        </div>
        <br />
        <span id="prod-company">{{sku}} {{manu}}</span>
        <br />
        <br />
        <div id="prod-desc">
          <span id="prod-abt">About the Product</span>
          <div id="prod-abt-dtls">{{desc}}</div>
          <button @click="addProduct()" id="btn-add-cart">ADD TO CART</button>
          <notifications group="foo" width="400px" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import arrow from "@/assets/images/arrow.png";
import arrowL from "@/assets/images/arrow-l.png";
export default {
  name: "ProductSelector",
  props: {
    cartItems: Array
  },
  data: () => {
    {
      return {
        arrow,
        arrowL,
        classA: {
          backgroundColor: "rgba(134, 134, 134, 0.900)",
          transform: "scale(1.3)",
          transition: "0.3s"
        },
        classB: {
          backgroundColor: "rgba(134, 134, 134, 0.404)"
        },
        products: [],
        currentProduct: [],
        image: null,
        sku: null,
        name: null,
        manu: null,
        desc: null,
        currentNumber: 1,
        timer: null
      };
    }
  },
  mounted: function() {
    this.$nextTick(function() {
      this.getProducts();
      this.startRotation();
    });
  },
  watch: {
    products: function() {
      this.sortProducts(this.currentNumber);
    },
    currentProduct: function() {
      this.currentImage();
      this.currentName();
      this.currentSku();
      this.currentDesc();
      this.currentManu();
    },
    currentNumber: function() {
      this.sortProducts(this.currentNumber);
    }
  },
  methods: {
    //Get and sort products into carousel.
    getProducts: function() {
      let vm = this;
      axios
        .get("https://my-json-server.typicode.com/simpatra/mockapi/products")
        .then(res => {
          vm.products = res.data;
        });
    },
    sortProducts: function(current) {
      let newArr = [];
      this.products.map(e => {
        if (e.id === current) {
          for (const val in e) {
            newArr.push(e[val]);
          }
        }
      });
      this.currentProduct = newArr;
    },
    //Addproduct after checking cart for already existing.
    addProduct: function() {
      let vm = this;
      let newArr = [{ favorite: false }, { quantity: 1 }];
      let checkRes = false;
      let addProductFn = function() {
        vm.products.map(e => {
          if (e.id === vm.currentNumber) {
            for (let val in e) {
              newArr.push(e[val]);
            }
            vm.cartItems.push(newArr);
          }
        });
        vm.$notify({
          group: "foo",
          type: "success",
          title: "Success!",
          text: "Item has been added to the cart!"
        });
      };
      let checkCart = function() {
        vm.cartItems.map(e => {
          for (let val in e) {
            if (e[val] === vm.currentNumber) {
              checkRes = true;
            }
          }
        });
      };
      checkCart();
      checkRes !== true
        ? addProductFn()
        : vm.$notify({
            group: "foo",
            type: "error",
            title: "Warning.",
            text: "Item is already in the cart."
          });
    },
    carouselNav: function(index) {
      this.currentNumber = index;
    },
    //Set products into carousel.
    currentImage: function() {
      let val;
      this.currentProduct.map((e, i) => {
        if (i === 5) {
          val = e;
        }
      });
      this.image = val[0].url;
    },
    currentSku: function() {
      let val;
      this.currentProduct.map((e, i) => {
        if (i === 2) {
          val = e;
        }
      });
      this.sku = val;
    },
    currentDesc: function() {
      let val;
      this.currentProduct.map((e, i) => {
        if (i === 6) {
          val = e;
        }
      });
      this.desc = val;
    },
    currentManu: function() {
      let val;
      this.currentProduct.map((e, i) => {
        if (i === 4) {
          val = e;
        }
      });
      this.manu = val;
    },
    currentName: function() {
      let val;
      this.currentProduct.map((e, i) => {
        if (i === 1) {
          val = e;
        }
      });
      this.name = val;
    },
    // Carousel Functionality
    startRotation: function() {
      this.timer = setInterval(this.next, 3000);
    },
    stopRotation: function() {
      clearTimeout(this.timer);
      this.timer = null;
    },
    next: function() {
      if (this.currentNumber >= this.products.length) {
        this.currentNumber = 1;
      } else {
        this.currentNumber += 1;
      }
    },
    prev: function() {
      if (this.currentNumber === 1) {
        this.currentNumber = this.products.length;
      } else {
        this.currentNumber -= 1;
      }
    }
  }
};
</script>
<style>
#product-s-cont {
  display: flex;
  padding: 40px;
  position: relative;
  align-items: center;
  justify-content: space-between;
}
#num-container {
  display: flex;
  position: absolute;
  justify-content: space-around;
  align-items: center;
  width: 740px;
  height: 70px;
  top: 0;
  right: 0;
  margin-top: 20px;
  margin-right: 275px;
  padding: 5px 20px;
}
.num {
  height: 60px;
  width: 60px;
  border-radius: 50%;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 18px;
}
.num:hover {
  cursor: pointer;
}
#btn-arrow-r {
  background: none;
  position: absolute;
  object-fit: center;
  height: 150px;
  width: 100px;
  background: transparent;
  border: none;
  right: 0;
}
#btn-arrow-l {
  background: none;
  position: absolute;
  object-fit: center;
  height: 150px;
  width: 100px;
  background: transparent;
  border: none;
  left: 0;
}
#btn-arrow-l:hover,
#btn-arrow-r:hover {
  transform: scale(0.7);
  transition: 0.2s;
  cursor: pointer;
}
#img-cont {
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  height: 650px;
  width: 450px;
}
#product-cont {
  height: 80%;
  width: 100%;
  margin-left: 100px;
  object-fit: contain;
}
#prod-dtls {
  display: flex;
  position: relative;
  flex-direction: column;
  width: 730px;
  height: 465px;
  margin-right: 100px;
}
#sku {
  font-weight: 700;
  margin-left: 50px;
  height: 410px;
  overflow: scroll;
  font-size: 22px;
}
#prod-abt {
  font-size: 20px;
  font-weight: 700;
  color: rgba(0, 0, 0, 0.541);
  letter-spacing: 0.1px;
}
#prod-abt-dtls {
  line-height: 35px;
  font-weight: 500;
  margin-top: 10px;
}
#o-prod {
  color: rgba(255, 72, 0, 0.801);
}
#o-prod {
  cursor: pointer;
}
#b-prod {
  color: rgba(0, 0, 0, 0.582);
}
#prod-company {
  font-size: 15px;
  font-weight: 600;
  color: rgba(0, 0, 0, 0.486);
}
#btn-add-cart {
  width: 230px;
  position: absolute;
  bottom: 0;
  margin-bottom: -75px;
  border: none;
  color: white;
  border-radius: 10px;
  font-size: 16px;
  height: 50px;
  background-color: rgba(235, 66, 0, 0.801);
}
#btn-add-cart:hover {
  background-color: rgba(255, 156, 42, 0.897);
  cursor: pointer;
  transition: 0.3s;
  transform: scale(1.1);
  transition: 0.2s;
}
</style>
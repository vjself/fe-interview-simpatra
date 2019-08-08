<template>
  <div id="cart-cont">
    <notifications group="foo" width="400px" />
    <div id="item-amount">
      <span id="cart-t">Cart Details&nbsp;&nbsp;</span>
      <span id="item-num">({{cartItems.length === 0 ? 0 : cartItems.length}} Items)</span>
    </div>
    <div id="item-list">
      <div class="item" v-for="(item, i) in cartItems" :key="i">
        <!-- Item Picture -->
        <img id="pic" :src="item[7][0].url" />
        <div class="cart-name-box">
          <!-- Sku and brand name box -->
          <div class="item-sku">
            <b>{{item[4]}}</b>
          </div>
          <div class="item-name">{{item[3]}}</div>
        </div>
        <!-- Quantity buttons -->
        <div class="quantity">
          <button @click="minusItem(item[2])" id="minus-button">-</button>
          <div id="quantity-num">{{item[1].quantity}}</div>
          <button @click="plusItem(item[2])" id="plus-button">+</button>
        </div>
        <!-- Price of item(accumulated) -->
        <div class="price">
          <b>{{Math.round(item[5])}}</b>
        </div>
        <div class="fav-trash">
          <div
            class="fav"
            v-show="item[0].favorite === true"
            v-bind:style="{ backgroundImage: 'url(' + starFilled + ')' }"
            @click="toggleFav(item[2])"
          ></div>
          <div
            class="fav"
            v-show="item[0].favorite === false"
            v-bind:style="{ backgroundImage: 'url(' + star + ')' }"
            @click="toggleFav(item[2])"
          ></div>
          <div
            id="trash"
            v-bind:style="{ backgroundImage: 'url(' + trash + ')' }"
            @click="trashItem(item[2])"
          ></div>
        </div>
      </div>
    </div>
    <button id="checkout" v-if="cartItems.length">CHECKOUT</button>
  </div>
</template>

<script>
import bottle from "@/assets/images/bottle.png";
import star from "@/assets/images/star.png";
import starFilled from "@/assets/images/star-filled.png";
import trash from "@/assets/images/trash.png";
export default {
  name: "DropCart",
  template: "drop-cart",
  props: {
    cartItems: Array
  },
  data: () => {
    return {
      star,
      starFilled,
      bottle,
      trash
    };
  },
  methods: {
    plusItem: function(index) {
      this.cartItems.forEach(e => {
        if (index === e[2]) {
          e[1].quantity += 1;
        }
      });
    },
    minusItem: function(index) {
      this.cartItems.forEach(e => {
        if (index === e[2]) {
          if (e[1].quantity === 1) {
            this.trashItem(index);
          } else {
            e[1].quantity -= 1;
          }
        }
      });
    },
    trashItem: function(index) {
      this.cartItems.forEach(e => {
        if (index === e[2]) {
          this.cartItems.splice(e, 1);
          this.$notify({
            group: "foo",
            type: "warn",
            title: "Success!",
            text: "Item removed from cart."
          });
        } else if (index < 1) {
          this.cartItems = [];
        }
      });
    },
    toggleFav: function(index) {
      this.cartItems.forEach(e => {
        if (index === e[2]) {
          if (e[0].favorite === false) {
            this.$notify({
              group: "foo",
              type: "success",
              title: "Success!",
              text: "Item added to favorites!"
            });
          } else {
            this.$notify({
              group: "foo",
              type: "warn",
              title: "Success!",
              text: "Item removed from favorites!"
            });
          }
          return (e[0].favorite = !e[0].favorite);
        }
      });
    }
  }
};
</script>
<style>
#cart-cont {
  display: flex;
  flex-direction: column;
  padding: 10px 25px;
  position: absolute;
  right: 0;
  border-radius: 10px;
  background-color: white;
  z-index: 1;
  margin-top: 150px;
  margin-right: 100px;
  width: 450px;
  box-shadow: 0px 3px 8px rgba(0, 0, 0, 0.644);
}

#item-amount {
  display: flex;
  height: 80px;
  align-items: center;
  width: 100%;
  margin-top: 5px;
}

#cart-t {
  font-size: 36px;
  color: rgba(0, 0, 0, 0.644);
}

#item-num {
  font-size: 19px;
  color: rgba(0, 0, 0, 0.644);
}

#item-list {
  display: flex;
  flex-direction: column;
  height: 80%;
}

.item {
  display: flex;
  position: relative;
  flex-direction: row;
  height: 80px;

  align-items: bottom;
  justify-content: space-between;
  width: 100%;
  align-items: center;
  border-bottom: dotted 3px rgba(0, 0, 0, 0.397);
}

#pic {
  height: 40px;
  width: 40px;
  border-radius: 50%;
  object-fit: contain;
}

.item-sku {
  color: rgb(255, 72, 0);
  margin-bottom: 10px;
}

.item-name {
  font-size: 9px;
  font-weight: 600px;
  width: 85px;
  max-height: 50px;
  overflow-y: scroll;
}

.price {
  color: rgb(255, 72, 0);
  width: 12px;
}

.quantity > button {
  border: none;
  background: none;
  font-size: 18px;
  padding: 0;
}

.quantity > button:focus {
  outline: none;
}

#minus-button {
  font-size: 25px;
  margin-bottom: 1px;
}

#minus-button:hover {
  transform: scale(1.7);
  cursor: pointer;
  transition: 0.2s;
}

#plus-button:hover {
  transform: scale(1.7);
  cursor: pointer;
  transition: 0.2s;
}

.quantity {
  display: flex;
  justify-content: space-around;
  background-color: rgba(128, 128, 128, 0.178);
  align-items: center;
  border-radius: 7px;
  height: 30px;
  width: 75px;
}

.fav-trash {
  display: flex;
  justify-content: space-between;
  height: 20px;
  width: 45px;
}

.fav {
  background-size: contain;
  height: 100%;
  width: 18px;
  height: 16px;
  z-index: 2;
}

.fav:hover {
  transform: scale(1.3);
  outline-color: rgb(255, 153, 0);
  transition: 0.2s;
  cursor: pointer;
}

#trash:hover {
  transform: scale(1.3);
  transition: 0.2s;

  outline-color: rgb(255, 153, 0);
  cursor: pointer;
}

#trash {
  background-size: contain;
  height: 100%;
  width: 19px;
  height: 19px;
}

.fav-trash img {
  height: 19px;
  width: 20px;
  background: center;
}

#quantity-num {
  font-size: 10px;
  font-weight: 700;
}

#checkout:hover {
  background-color: rgb(245, 126, 58);
  transition: 0.2s;
  transform: scale(1.025);
  transition: 0.2s;
  cursor: pointer;
}

#checkout {
  bottom: 0;
  font-size: 24px;
  margin: 20px 0px;
  font-weight: 600;
  height: 50px;
  width: 100%;
  border: none;
  color: white;
  border-radius: 5px;
  padding: 5px;
  background-color: rgb(243, 94, 35);
}
</style>

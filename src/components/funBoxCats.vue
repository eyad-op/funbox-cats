<template>
  <div class="main">
    <h1>Ты сегодня покормил кота?</h1>
    <div class="products">
      <div v-for="(product, index) in products" class="product" :key="index">
        <div
          :style="
            product.isSelected
              ? selectedStyle
              : !product.inStock
              ? disabledStyle
              : null
          "
          class="product__container"
          @click="
            product.inStock ? (product.isSelected = !product.isSelected) : null
          "
        >
          <span
            class="product__container-corner"
            :style="product.isSelected ? selectedStyle : null"
          ></span>
          <p class="product__title">{{ product.title }}</p>
          <h2 class="product__name">{{ product.name }}</h2>
          <h3 class="product__taste">{{ product.taste }}</h3>
          <p class="product__portion">
            <span class="product__portion-quantity">{{
              product.portionsQuantity
            }}</span>
            {{ product.portions }}
          </p>
          <p class="product__gift">
            <span class="product__gift-quantity">{{
              product.giftQuantity
            }}</span>
            {{ product.gift }}
          </p>
          <p v-if="product.isHappy" class="product__gift-happy">
            заказчик доволен
          </p>
          <span
            :style="product.isSelected ? { background: '#D91667' } : null"
            class="product__weight"
          >
            <span class="product__weight-number">{{ product.weight }}</span>
            КГ</span
          >
        </div>
        <p v-if="!product.isSelected && product.inStock" class="product__buy">
          Чего сидишь? Порадуй котэ,
          <a
            @click="product.inStock = !product.inStock"
            href="/"
            v-on:click.prevent
            class="product__buy-btn"
          >
            купи.</a
          >
        </p>
        <p
          v-else-if="product.isSelected && product.inStock"
          class="product__buy"
        >
          {{ product.isSelectedText }}
        </p>
        <p v-if="!product.inStock" class="product__buy" style="color: #ffff66">
          {{ product.outOfStockText }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { productsData } from "@/assets/data";
export default {
  data() {
    return {
      products: productsData,
      selectedStyle: {
        border: "4px solid #D91667",
      },
      disabledStyle: {
        filter: "grayscale(1)",
        "pointer-events": "none",
        color: "#B3B3B3",
      },
    };
  },
};
</script>

<style lang="scss">
@font-face {
  font-family: "Trebuchet MS";
  src: local("Trebuchet MS"), url(../assets/fonts/trebuc.ttf) format("ttf");
}
@import url("https://fonts.googleapis.com/css2?family=Exo+2:wght@100;200;300&display=swap");
*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  color: #fff;
  background: url(../assets/images/Pattern.png) center/cover no-repeat;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main {
  font-family: "Trebuchet MS", sans-serif;
  max-width: 1280px;
  & h1 {
    font-family: "Exo 2", sans-serif;
    font-weight: 100;
    text-align: center;
    font-size: 36px;
    line-height: 44px;
  }
  @media (max-width: 1150px) {
    width: 100%;
    padding: 30px 0;
  }
}
.products {
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  gap: 80px;
  margin-top: 24px;
  @media (max-width: 1150px) {
    flex-wrap: wrap;
  }
}
.product {
  gap: 20px;
  @media (max-width: 768px) {
    flex: 0 1 0;
  }
  &__container {
    position: relative;
    width: 320px;
    height: 480px;
    padding: 21px 51px;
    border: 4px solid #1698d9;
    border-radius: 10px;
    color: #000;
    clip-path: polygon(15% 0, 100% 0, 100% 100%, 0 100%, 0 10%);
    background: url(../assets/images/cat.png) no-repeat;
    background-position: bottom left;
    background-size: contain;
    background-color: #fff;
    transition: 0.3s;

    &-corner {
      display: block;
      position: absolute;
      width: 64px;
      height: 64px;
      top: 0;
      left: 0;
      transform: translate(-50%, -50%) rotate(45deg);
      background: #1698d9;
      transition: 0.3s;
    }
    &:hover {
      transform: scale(1.05);
      filter: brightness(1.1) contrast(1.1);
    }
  }

  &__title {
    font-size: 16px;
    font-weight: 400;
    color: #666666;
  }
  &__name {
    font-size: 48px;
    margin-top: 5px;
    line-height: 56px;
  }
  &__taste {
    font-size: 24px;
    line-height: 28px;
  }
  &__portion {
    margin-top: 15px;
    font-size: 14px;
    color: #666666;
    &-quantity {
      font-weight: 600;
    }
  }
  &__gift {
    font-size: 14px;
    color: #666666;
    &-quantity {
      font-weight: 600;
    }
    &-happy {
      font-size: 14px;
      color: #666666;
    }
  }
  &__weight {
    display: block;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: absolute;
    bottom: 16px;
    right: 16px;
    background-color: #1698d9;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    color: #fff;
    font-size: 16px;
    font-weight: 400;
    transition: 0.3s;
    &-number {
      font-size: 42px;
    }
  }
  &__buy {
    margin-top: 14px;
    font-size: 13px;
    line-height: 15px;
    text-align: center;
    &-btn {
      color: #1698d9;
      text-decoration-style: dashed;
    }
  }
}
</style>

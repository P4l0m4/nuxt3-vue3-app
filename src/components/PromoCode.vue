<script setup>
import { useCartStore } from '@/stores/cart'
const cartStore = useCartStore()
</script>
<template>
  <div class="promo">
    <label for="code">Code promo</label>
    <div class="promo__test">
      <div class="promo__test__wrapper">
        <input placeholder="Code promo" id="code" class="promo__test__wrapper__input" v-model="codeToTry" />
        <button class="promo__test__wrapper__button" type="submit" @click="cartStore.addPromoCode(codeToTry)">
          Tester
        </button>
      </div>
      <div class="promo__test__codes" v-if="cartStore.checkout.discountApplications?.length > 0">
        Code(s) promo appliqué(s)
        <span
          class="promo__test__codes__code"
          v-for="discount in cartStore.checkout.discountApplications"
          :key="discount.code"
        >
          {{ discount.code }}
        </span>
      </div>
    </div>
    <div class="promo__error" v-if="cartStore.checkout.userErrors?.length > 0">
      Le code <span class="promo__error__code">{{ codeToTry }}</span> est invalide.
    </div>
  </div>
</template>

<style lang="scss" scoped>
.promo {
  display: flex;
  background-color: $primary-color;
  padding: 16px;
  flex-direction: column;
  gap: 32px;
  font-size: 20px;
  width: 100%;
  border-radius: 6px;

  &__test {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 100%;
    align-items: flex-start;

    &__wrapper {
      display: flex;
      gap: 8px;
      max-height: 40px;
      width: clamp(100px, 100%, 444px);

      &__input {
        padding: 8px;
        background-color: $primary-color;
        outline: none;
        border: white 2px solid;
        width: clamp(100px, 100%, 375px);
      }

      &__button {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 8px;
        cursor: pointer;
        background-color: $secondary-color;
        color: black;
        font-weight: 600;
        border: $secondary-color solid 2px;
      }
    }

    &__codes {
      display: flex;
      gap: 8px;
      flex-direction: column;
      font-size: 16px;

      &__code {
        font-size: 16px;
        display: flex;
        padding: 8px 16px;
        border: #006400 solid 2px;
        border-radius: 6px;
        color: #006400;
        font-weight: 700;
        justify-content: center;
      }
    }
  }
  &__error {
    color: red;
    font-size: 16px;

    &__code {
      text-transform: uppercase;
      color: red;
    }
  }
}
</style>

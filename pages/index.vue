<template>
  <div class="container-w">
    <div class="button-wrapper flex flex-col justify-center items-center px-3">
      <div v-if="!isUserAuth" class="px-3 w-full flex flex-col gap-2.5">
        <UiButton :button-name="'Registration'" @click="setIsLogin(false)" />
        <UiButton :button-name="'Login'" @click="setIsLogin(true)" />
      </div>
      <div v-if="isUserAuth" class="text-white font-semibold text-5xl">
        Hellow!
      </div>
      <NuxtLink
        v-if="isUserAuth"
        class="link-to-orders font-semibold flex flex-col justify-center hover:scale-101 items-center w-full transition delay-150 duration-300 ease-in-out hover:-translate-y-1"
        to="/orders"
        >Orders</NuxtLink
      >
    </div>
    <Auth v-if="isAuth" :is-login="isLogin" @close-auth="isAuth = false" />
  </div>
</template>
<script setup lang="ts">
import { useAuthStore, useIsLoadingStore } from '~/store/auth.store';

definePageMeta({
  title: 'Orders',
});
const authStore = useAuthStore();
const looadingStore = useIsLoadingStore();

const isLoading = computed(() => looadingStore.isLoading);
const isUserAuth = computed(() => authStore.isAuth);

const isLogin = ref(false);
const isAuth = ref(false);
const setIsLogin = (status: boolean) => {
  isLogin.value = status;
  isAuth.value = true;
};
</script>
<style lang="scss" scoped>
.link-to-orders {
  background-color: $bg-button-main;
  width: 100%;
  padding: 12px;
  font-size: 12px;
  border-radius: 24px;
  font-weight: 700;
  margin-top: 40px;
}
.button-wrapper {
  min-height: 90vh;
}
</style>

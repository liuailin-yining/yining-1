

<template>
  <!-- <router-view></router-view> -->
  <!-- <router-link to="/map"></router-link>
  <router-link to="/chart"></router-link> -->
  <a-config-provider :locale="zhCN">
      <router-link to="/logo"></router-link>
      <router-view></router-view>
  </a-config-provider>

</template>
<script  lang="ts">
import zhCN from 'ant-design-vue/es/locale/zh_CN';
import dayjs from 'dayjs';
import { defineComponent, ref, watch } from 'vue';
import 'dayjs/locale/zh-cn';
// dayjs.locale('cn');
export default {
     setup() {
        const locale = ref(zhCN.locale);
        watch(locale, val => {
          dayjs.locale(val);
        });
      return{
        locale,
        dayjs,
        zhCN,
      }

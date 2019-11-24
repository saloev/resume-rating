<template>
  <v-app>
    <top-header></top-header>

    <div class="pt-10">
      <resume-list></resume-list>
    </div>
  </v-app>
</template>

<script>
import TopHeader from '@/components/TopHeader.vue';
import ResumeList from '@/components/ResumeList.vue';

export default {
  name: 'App',

  components: {
    ResumeList,
    TopHeader,
  },

  data: () => ({
    //
  }),
};
</script>

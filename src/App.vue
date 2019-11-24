<template>
  <v-app>
    <resume-list></resume-list>
  </v-app>
</template>

<script>
import ResumeList from '@/components/ResumeList.vue';

export default {
  name: 'App',

  components: {
    ResumeList,
  },

  data: () => ({
    //
  }),
};
</script>

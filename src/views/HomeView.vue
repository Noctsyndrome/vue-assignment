<template>
  <div class="home-view">
    <ScheduleCalendar />
  </div>
</template>

<script>
import ScheduleCalendar from "@/components/ScheduleCalendar.vue";

export default {
  name: "HomeView",
  components: {
    ScheduleCalendar,
  },
};
</script>

<style lang="scss">
  .home-view {
    display: flex;
    width: 1280px;
    height: 720px;
    border: 2px solid #607d8b;
    border-radius: 12px;
    box-sizing: border-box;
    padding: 12px;
    margin: 80px auto;
  }
</style>
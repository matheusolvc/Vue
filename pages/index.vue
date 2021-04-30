<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<template>
  <div class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <div class="top-row">
      <h1 class="leads__title">Leads</h1>
    </div>
    <section>
      <leads-table></leads-table>
    </section>
  </div>
</template>

<script>
import LeadsTable from '~/components/LeadsTable.vue'
export default {
  components: { LeadsTable },
}
</script>

<style lang="scss" scoped="true">
.leads {
  &__title {
    margin: 1.4rem 0;
    padding: 1.4rem 0;
    border-top: $border-color 1px solid;
  }
}
.top-row {
  display: flex;
}
</style>

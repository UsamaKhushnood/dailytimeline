<template>
  <div class="main-container">
    <div class="records-table">
      <b-table
        borderless
        striped
        :items="items"
        thead-class="RTHead"
        tbody-class="RTBody"
      >
      </b-table>
    </div>
  </div>
</template>

<script>
export default {
  name: "Records",
  data: () => ({
    items: [
      { first_name: "Dickerson", last_name: "Macdonald" },
      { first_name: "Larsen", last_name: "Shaw" },
      { first_name: "Geneva", last_name: "Wilson" },
      { first_name: "Jami", last_name: "Carney" },
    ],
  }),
};
</script>
<style lang="scss">
.records-table {
  .RTHead {
    background-color: #18191c;
    th {
      color: #f1c40f;
    }
  }
  .RTBody {
    tr:nth-of-type(odd) {
      background-color: #3f4347 !important;
    }
    td {
      color: #fff;
    }
  }
}
</style>
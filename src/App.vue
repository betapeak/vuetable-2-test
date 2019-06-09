<template>
  <div>
    <vuetable
            ref="vuetable"
            api-url="https://vuetable.ratiw.net/api/users"
            :fields="fields"
            data-path="data"
            pagination-path=""
            @vuetable:pagination-data="onPaginationData"
            :css="BootstrapStyle.table"
            :show-sort-icons="true"
    >
    </vuetable>
    <vuetable-pagination
            ref="pagination"
            :css="BootstrapStyle.pagination"
            @vuetable-pagination:change-page="onChangePage"
    ></vuetable-pagination>
  </div>
</template>

<script>
import Vuetable from 'vuetable-2';
import VuetablePagination from 'vuetable-2/src/components/VuetablePagination'
import BootstrapStyle from './bootstrap-css.js';
import '../node_modules/bootstrap/dist/css/bootstrap.css';

export default {
  components: {
    Vuetable,
    VuetablePagination
  },

  data() {
    return {
      BootstrapStyle,
      fields: [
        'name', 'nickname', 'gender',
        {
          name: 'email',
          sortField: 'email'
        }
      ]
    }
  },

  methods: {
    //...
    // when the pagination data is available, set it to pagination component
    onPaginationData(paginationData) {
      this.$refs.pagination.setPaginationData(paginationData);
    },

    // when the user click something that causes the page to change,
    // call "changePage" method in Vuetable, so that that page will be
    // requested from the API endpoint.
    onChangePage(page) {
      this.$refs.vuetable.changePage(page);
    }
  }
};
</script>
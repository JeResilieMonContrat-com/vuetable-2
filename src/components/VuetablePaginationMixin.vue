<script>
export default {
  props: {
    css: {
      type: Object,
      default () {
        return {
          wrapperClass: 'ui right floated pagination menu',
          activeClass: 'active large',
          disabledClass: 'disabled',
          pageClass: 'item',
          linkClass: 'icon item',
          paginationClass: 'ui bottom attached segment grid',
          paginationInfoClass: 'left floated left aligned six wide column',
          dropdownClass: 'ui search dropdown',
          icons: {
            first: 'angle double left icon',
            prev: 'left chevron icon',
            next: 'right chevron icon',
            last: 'angle double right icon',
          }
        }
      }
    },
    onEachSide: {
      type: Number,
      default () {
        return 2
      }
    },
    data: {
      type: Object
    },
    dataFields: {
      type: Object,
      default () {
        return {
          current_page: 'current_page',
          last_page: 'last_page',
          total: 'total',
          per_page: 'per_page'
        }
      }
    }
  },
  data: function() {
    return {
      eventPrefix: 'vuetable-pagination:'
    }
  },
  computed: {
    totalPage () {
      if (!this.data) {
        return 0;
      }

      if (this.getData('last_page')) {
        return this.getData('last_page');
      }
      return Math.ceil(this.getData('total') / this.getData('per_page'))
    },
    isOnFirstPage () {
      if (!this.data || !this.getData('current_page')) {
        return true;
      }
      return this.getData('current_page') === 1;
    },
    isOnLastPage () {
      if (!this.data || !this.getData('last_page') || !this.getData('current_page')) {
        return false;
      }
      return this.getData('current_page') === this.getData('last_page');
    },
    notEnoughPages () {
      return this.totalPage < (this.onEachSide * 2) + 4
    },
    windowSize () {
      return this.onEachSide * 2 +1;
    },
    windowStart () {
      if (!this.data || !this.getData('current_page') || this.getData('current_page') <= this.onEachSide) {
        return 1
      } else if (this.getData('current_page') >= (this.totalPage - this.onEachSide)) {
        return this.totalPage - this.onEachSide*2
      }

      return this.getData('current_page') - this.onEachSide
    },
  },
  methods: {
    getData: function(name) {
      return this.data[this.dataFields[name]];
    },
    loadPage (page) {
      this.$emit(this.eventPrefix+'change-page', page)
    },
    isCurrentPage (page) {
      return page === this.getData('current_page')
    },
    setPaginationData (data) {
      this.data = data
    },
    resetData () {
      this.data = null
    }
  }
}
</script>

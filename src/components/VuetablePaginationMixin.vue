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
    }
  },
  data: function() {
    return {
      eventPrefix: 'vuetable-pagination:'
    }
  },
  computed: {
    totalPage () {
      if (!this.data || !this.data.last_page) {
        return 0;
      }
      return this.data.last_page;
    },
    isOnFirstPage () {
      if (!this.data || !this.data.current_page) {
        return true;
      }
      return this.data.current_page === 1;
    },
    isOnLastPage () {
      if (!this.data || !this.data.last_page || !this.data.current_page) {
        return false;
      }
      return this.data.current_page === this.data.last_page;
    },
    notEnoughPages () {
      return this.totalPage < (this.onEachSide * 2) + 4
    },
    windowSize () {
      return this.onEachSide * 2 +1;
    },
    windowStart () {
      if (!this.data || !this.data.current_page || this.data.current_page <= this.onEachSide) {
        return 1
      } else if (this.data.current_page >= (this.totalPage - this.onEachSide)) {
        return this.totalPage - this.onEachSide*2
      }

      return this.data.current_page - this.onEachSide
    },
  },
  methods: {
    loadPage (page) {
      this.$emit(this.eventPrefix+'change-page', page)
    },
    isCurrentPage (page) {
      return page === this.data.current_page
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

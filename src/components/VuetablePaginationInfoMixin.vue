<script>
export default {
  props: {
    css: {
      type: Object,
      default() {
        return {
          infoClass: 'left floated left aligned six wide column'
        }
      }
    },
    infoTemplate: {
      type: String,
      default() {
        return "Displaying {from} to {to} of {total} items"
      }
    },
    noDataTemplate: {
      type: String,
      default() {
        return 'No relevant data'
      }
    },
    data: {
      type: Object
    },
    dataFields: {
      type: Object,
      default() {
        return {
          current_page: 'current_page',
          last_page: 'last_page',
          total: 'total',
          from: 'from',
          to: 'to',
        }
      }
    }
  },
  computed: {
    lastPage () {
      return Math.ceil(this.getData('total') / this.getData('per_page'))
    },
    paginationInfo () {
      if (this.data == null || this.getData('total') == 0) {
        return this.noDataTemplate
      }

      return this.infoTemplate
        .replace('{from}', this.getData('from') || 0)
        .replace('{to}', this.getData('to') || 0)
        .replace('{total}', this.getData('total') || 0)
        .replace('{current}', this.getData('current_page') || 0)
        .replace('{last}', this.getData('last_page') || this.lastPage || 0)
    },
  },
  methods: {
    getData: function(name) {
      return this.data[this.dataFields[name]];
    },
    setPaginationData (data) {
      this.data = data
    },
    resetData () {
      this.data = null
    }
  },
}
</script>

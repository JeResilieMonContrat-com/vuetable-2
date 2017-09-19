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
    }
  },
  computed: {
    paginationInfo () {
      if (this.data == null || this.data.total == 0) {
        return this.noDataTemplate
      }

      return this.infoTemplate
        .replace('{from}', this.data.from || 0)
        .replace('{to}', this.data.to || 0)
        .replace('{total}', this.data.total || 0)
        .replace('{current}', this.data.current_page || 0)
        .replace('{last}', this.data.last_page || 0)
    },
  },
  methods: {
    setPaginationData (data) {
      this.data = data
    },
    resetData () {
      this.data = null
    }
  },
}
</script>

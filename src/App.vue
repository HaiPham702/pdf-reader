<template>
  <div>
    <PDFViewer :src="pdfUrl" />
  </div>
</template>

<script>
import PDFViewer from './components/PDFViewer.vue'

export default {
  name: 'App',
  components: {
    PDFViewer
  },
  data() {
    return {
      pdfUrl: '../pdfcoffee.com-sql-performance-explainedpdf.pdf'
    }
  }
}
</script>

<style>
/* Các kiểu CSS cho ứng dụng */
</style>

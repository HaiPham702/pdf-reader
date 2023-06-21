<template>
    <div>
      <div ref="pdfContainer"></div>
    </div>
  </template>
  
  <script>
import * as pdfjsLib from 'pdfjs-dist/legacy/build/pdf';

pdfjsLib.GlobalWorkerOptions.workerSrc = `${process.env.BASE_URL}workers/pdf.worker.js`;
  export default {
    name: 'PDFViewer',
    props: {
      src: {
        type: String,
        required: true
      }
    },
    mounted() {
      this.loadPDF()
    },
    methods: {
      async loadPDF() {
        const workerSrc = 'path/to/pdf.worker.js'; // Đường dẫn tới tệp pdf.worker.js
  
        const loadingTask = pdfjsLib.getDocument({
          url: this.src,
          worker: { src: workerSrc }
        });
  
        const pdf = await loadingTask.promise;
        const page = await pdf.getPage(1);
  
        const canvas = document.createElement('canvas');
        const context = canvas.getContext('2d');
        const viewport = page.getViewport({ scale: 1 });
  
        canvas.height = viewport.height;
        canvas.width = viewport.width;
  
        const renderContext = {
          canvasContext: context,
          viewport: viewport
        };
  
        await page.render(renderContext);
  
        this.$refs.pdfContainer.appendChild(canvas);
      }
    }
  }
  </script>
  
  <style scoped>
  canvas {
    border: 1px solid black;
  }
  </style>
  
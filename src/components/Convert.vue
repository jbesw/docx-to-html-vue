<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      This application runs in your browser and does not upload any files to any remote servers. Nothing leaves your browser.
    </p>
    <div>
      <input type="file" @change="onFileChange">
    </div>
    <div>
      <p class="htmlOutput">{{ htmlOutput }}</p>
    </div>
    <h3>Questions?</h3>
    <p>Contact <a href="https://twitter.com/jbesw/">@jbesw</a> on Twitter.</p>
  </div>
</template>

<script>

const mammoth = require("mammoth")
const cheerio = require('cheerio')
const options = { convertImage: mammoth.images.imgElement() }

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function () {
    return {
      image: '',
      htmlOutput: 'Output appears here.'
    }
  },
  methods: {
    onFileChange: async function (e) {
      let files = e.target.files || e.dataTransfer.files
      if (!files.length) return
      let reader = new FileReader()
      console.log(files[0])
      let that = this

      reader.onload = async function(loadEvent) {
        console.log('onload: ', event)
        const arrayBuffer = loadEvent.target.result
        console.log('buffer: ', arrayBuffer)
        const result = await mammoth.convertToHtml({ arrayBuffer }, options)
        console.log('result: ', result)
        const $ = cheerio.load(result.value)
        $('a').attr('target','_blank')
        $('a').attr('rel','noopener')
        that.htmlOutput = $.html()
      }

			reader.readAsArrayBuffer(files[0])
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
}
.htmlOutput {
  font-family: "Courier New", Courier, "Lucida Sans Typewriter";
  color: grey
}
</style>

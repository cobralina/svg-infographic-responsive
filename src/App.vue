<template>
<div class="global-wrapper">
<div class="form-wrapper">
  <form> 
    <div class="form-h1">Konfigurieren der Grafik</div>
    <div class="form-label">Headline:</div>
  <input class="input_generator" v-model="infoHeadline" id="infoHeadline" ><br>
  <div class="form-label">Subline:</div>
  <input class="input_generator" v-model="infoSubline" id="infoSubline" >
  <div class="form-label">HTML-Code SVG:</div>
  <input class="input_generator" v-model="svgCode" id="svgCode" >
 
  <div class="form-label">Höhe (ohne Eingabe =400px):</div>
  <input class="input_ticks" v-model="wrapperMaxHeight" id="wrapperMaxHeight" >
  <div class="form-label">Achsenticks X-Achse (min. 2):</div>
  <input class="input_ticks" v-model="x1" id="x1" >
  <input class="input_ticks" v-model="x2" id="x2" >
  <input class="input_ticks" v-model="x3" id="x3" >
  <input class="input_ticks" v-model="x4" id="x4" >
  <input class="input_ticks" v-model="x5" id="x5" >
  <input class="input_ticks" v-model="x6" id="x6" >
  <div class="form-label">Achsenticks Y-Achse (min. 2):</div>
  <input class="input_ticks" v-model="y1" id="y1" >
  <input class="input_ticks" v-model="y2" id="y2" >
  <input class="input_ticks" v-model="y3" id="y3" >
  <input class="input_ticks" v-model="y4" id="y4" >
  <input class="input_ticks" v-model="y5" id="y5" >
  <input class="input_ticks" v-model="y6" id="y6" >  <br>
  <br><br>
  <div class="form-label">Anmerkungen (optional):</div>
  <input class="input_generator" v-model="infoAnnotation" id="infoAnnotation" >
  <div class="form-label">Grafik:</div>
  <input class="input_generator" v-model="infoGraphic" id="infoGraphic" >
  <div class="form-label">Quelle:</div>
  <input class="input_generator" v-model="infoSource" id="infoSource" >
  <br><br>
  <div class="form-label">Legende (Alle Werte optional): <br><br>
  Hexwert &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Beschreibungstext&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Wert (fett) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Text nach Wert </div>
  <input class="input_colors" v-model="legendColor1" id="legendColor1" label="Farbe"> <input class="input_legend" v-model="legendLabel1" id="legendLabel1" ><input class="input_colors" v-model="legendValue1" id="legendValue1" /><input class="input_colors" v-model="legendTimestamp1" id="legendTimestamp1" /><br>
  <input class="input_colors" v-model="legendColor2" id="legendColor2" label="Farbe"> <input class="input_legend" v-model="legendLabel2" id="legendLabel2" ><input class="input_colors" v-model="legendValue2" id="legendValue2" /><input class="input_colors" v-model="legendTimestamp2" id="legendTimestamp2" /><br>
  <input class="input_colors" v-model="legendColor3" id="legendColor3" label="Farbe"> <input class="input_legend" v-model="legendLabel3" id="legendLabel3" ><input class="input_colors" v-model="legendValue3" id="legendValue3" /><input class="input_colors" v-model="legendTimestamp3" id="legendTimestamp3" /><br>
  <input class="input_colors" v-model="legendColor4" id="legendColor4" label="Farbe"> <input class="input_legend" v-model="legendLabel4" id="legendLabel4" ><input class="input_colors" v-model="legendValue4" id="legendValue4" /><input class="input_colors" v-model="legendTimestamp4" id="legendTimestamp4" /><br>
  <input class="input_colors" v-model="legendColor5" id="legendColor5" label="Farbe"> <input class="input_legend" v-model="legendLabel5" id="legendLabel5" ><input class="input_colors" v-model="legendValue5" id="legendValue5" /><input class="input_colors" v-model="legendTimestamp5" id="legendTimestamp5" /><br>
  <input class="input_colors" v-model="legendColor6" id="legendColor6" label="Farbe"> <input class="input_legend" v-model="legendLabel6" id="legendLabel6" ><input class="input_colors" v-model="legendValue6" id="legendValue6" /><input class="input_colors" v-model="legendTimestamp6" id="legendTimestamp6" /><br>
    <br>
  <br>
   <br>
  <br>

  <button class="gen_button" v-on:click.prevent="generateSourceCode">Abschicken</button>
</form>
</div>

  <div class="graphic-wrapper">   
    <div class="form-h1">Vorschau </div><br><br>
 <div class="info-wrapper">
  <div class="info-headline">{{ infoHeadline }}</div>
    <div class="info-subline">{{ infoSubline }}</div>
    <div class="info-legend" v-html="legendHTML">
    </div>
    <div class="first-box" >
        <div class="y-axis" id="y-axis" v-html = 'yHTML'>
        </div>
      <div class="svg-wrapper" v-html="newSvgCode" >
          </div>
        </div>
        <div class="second-box">
        <div class="x-axis" id="y-axis" v-html = 'xHTML'>
        </div>
        <div class="info-source">{{ infoAnnotation }} </div>  
        <div class="info-source">Grafik: {{ infoGraphic }} / Quelle: {{ infoSource }}</div>  
    </div>
        </div>
      </div>
      <div class="code-wrapper"> <span class="code-wrapper-no-copy"><div class="form-h1">HTML-Code zum Kopieren:</div></span> 
        <br><br>
        {{ copyHeaderCode }}
        {{ copySvgCode }} 
        {{ copyFooterCode }} 
       
      </div>
    </div>
</template>

<script>


export default {
  name: 'App',
  components: {
  },

  data () {
    return {
    wrapperMaxHeight:"",
    infoHeadline:"",
    infoSubline:"",
    infoAnnotation:"",
    infoGraphic:"",
    infoSource:"",
    legendColors:[],
    legendLabels:[],
    xLabels:[],
    yLabels:[],
     svgCode:"",
     splittedCode:"",
     newSvgCode:"",
     copySvGCode:"",
     x1:"",
     x2:"",
     x3:"",
     x4:"",
     x5:"",
     x6:"",
     y1:"",
     y2:"",
     y3:"",
     y4:"",
     y5:"",
     y6:"",
     xHTML:"",
     yHTML:"",
     copyHeaderCode:'',
     copyFooterCode:'',
     legendColor1:"",
     legendColor2:"",
     legendColor3:"",
     legendColor4:"",
     legendColor5:"",
     legendColor6:"",
     arrLegendColors:[],
     legendLabel1:"",
     legendLabel2:"",
     legendLabel3:"",
     legendLabel4:"",
     legendLabel5:"",
     legendLabel6:"",
     arrLegendLabels:[],
     legendHTML:"",
     legendTimestamp1:"",
     legendTimestamp2:"",
     legendTimestamp3:"",
     legendTimestamp4:"",
     legendTimestamp5:"",
     legendTimestamp6:"",
     arrLegendTimestamp:[],
     legendValue1:"",
     legendValue2:"",
     legendValue3:"",
     legendValue4:"",
     legendValue5:"",
     legendValue6:"",
     arrLegendValues:[],
     infoColorWidth:"15px"
    }
  },
  computed: {
    
  },
  methods: {
    generateSourceCode: function() {

      this.copyHeaderCode = "";
      this.copySvgCode = "";
      this.copyFooterCode = "";
      this.xHTML = "";
      this.yHTML = "";
      this.xLabels = [];
      this.yLabels = [];
      this.arrLegendColors = [];
      this.arrLegendLabels = [];
      this.arrLegendTimestamp = [];
      this.arrLegendValues = [];
      this.legendHTML = "";

      this.splittedCode = this.svgCode.split('viewBox=')[1];

    

      if (this.wrapperMaxHeight == "") {
        this.wrapperMaxHeight = "400"
      }

      if (this.wrapperMaxHeight.search("px") < 0) {
        this.wrapperMaxHeight = this.wrapperMaxHeight +"px";
      }

      this.newSvgCode='<svg preserveAspectRatio="none" id="linegraph" xmlns="http://www.w3.org/2000/svg" viewBox='+this.splittedCode;
      this.copySvgCode='<div class="svg-wrapper" height="'+ this.wrapperMaxHeight +'">'+this.newSvgCode+'</div></div>';

      this.xLabels.push(this.x1, this.x2, this.x3, this.x4, this.x5, this.x6);
      this.xLabels = this.xLabels.filter(String);

      this.yLabels.push(this.y1, this.y2, this.y3, this.y4, this.y5, this.y6);
      this.yLabels = this.yLabels.filter(String);

      var xcode = "";
      var xlen = this.xLabels.length;
      var i = 0

      for ( i = 0; i < xlen; i++ ) {
        xcode = xcode + '<div class="x-label">'+this.xLabels[i]+'</div>'
      }

      this.xHTML = xcode;

      var ycode = "";
      var ylen = this.yLabels.length;
      var j = 0

      for ( j = ylen-1; j >= 0; j-- ) {
        ycode = ycode + '<div class="y-label">'+this.yLabels[j]+'</div>'
      }

      this.yHTML = ycode;

      this.arrLegendColors.push(this.legendColor1, this.legendColor2, this.legendColor3, this.legendColor4, this.legendColor5, this.legendColor6);
      this.arrLegendColors = this.arrLegendColors.filter(String);

      this.arrLegendLabels.push(this.legendLabel1, this.legendLabel2, this.legendLabel3, this.legendLabel4, this.legendLabel5, this.legendLabel6);
      this.arrLegendLabels = this.arrLegendLabels.filter(String);

      this.arrLegendTimestamp.push(this.legendTimestamp1, this.legendTimestamp2, this.legendTimestamp3, this.legendTimestamp4, this.legendTimestamp5, this.legendTimestamp6);
      this.arrLegendTimestamp = this.arrLegendTimestamp.filter(String);

      this.arrLegendValues.push(this.legendValue1, this.legendValue2, this.legendValue3, this.legendValue4, this.legendValue5, this.legendValue6);
      this.arrLegendValues = this.arrLegendValues.filter(String);


      if (this.arrLegendColors.length == 0) {
        this.infoColorWidth = "0px";
      } else {
        this.infoColorWidth = "15px";
      }

      
      var legendcode = "";

      var arrLegendLen = [];
      
      arrLegendLen.push(this.arrLegendLabels.length, this.arrLegendColors.length, this.arrLegendTimestamp.length, this.arrLegendValues.length);
      var legendlen = Math.max(...arrLegendLen);

      console.log ("legendlen: " + legendlen);

      var k = 0

      for ( k = 0; k < legendlen; k++ ) {

        var colorStyle = 'style="color:'+ this.arrLegendColors[k] +'"';
        if (this.arrLegendColors[k] == undefined) {
          colorStyle="";
        }

        var divColor = '<div class="info-color" style="background-color:'+this.arrLegendColors[k]+';width:'+ this.infoColorWidth +'"></div>';
        var divDesc = '<div class="info-label">'+this.arrLegendLabels[k]+'</div>';
        var divValue = '<div class="info-value" ' + colorStyle +'>'+this.arrLegendValues[k]+'</div>';
        var divAfter = '<div class="info-label">'+this.arrLegendTimestamp[k]+'</div>';


        if (this.arrLegendColors[k] == undefined) {
          this.arrLegendColors[k]="";
          divColor = "";
        }
        if (this.arrLegendLabels[k] == undefined) {
          this.arrLegendLabels[k]="";
          divDesc = "";
        }
        if (this.arrLegendTimestamp[k] == undefined) {
          this.arrLegendTimestamp[k]="";
          divAfter = "";
        }
        if (this.arrLegendValues[k] == undefined) {
          this.arrLegendValues[k]="";
          divValue = "";
        }

        
        legendcode = legendcode + '<div class="legend-item">' + divColor + divDesc + divValue + divAfter + '</div>'
        this.legendHTML = '<div class="info-legend">' + legendcode + '</div>'

        if (legendlen == 0) {
          console.log("no legend");
          legendcode = "";
          this.legendHTML = "";
        }
      }


      var divHeadline = '<div class="info-headline">'+ this.infoHeadline +'</div>';
      if (this.infoHeadline == "") {
        divHeadline = "";
      }

      var divSubline = '<div class="info-subline">'+ this.infoSubline +'</div>';
      if (this.infoSubline == "") {
        divSubline = "";
      }
      console.log(divSubline)

      var divY = '<div class="y-axis" height="'+ this.wrapperMaxHeight +'" id="y-axis">'+ this.yHTML + '</div>'
      if (this.yHTML =="") {
        divY = "";
      }

      var divX ='<div class="second-box"><div class="x-axis" id="x-axis">' + this.xHTML + '</div></div>'
      if (this.xHTML ==""){
        divX ="";
      }

      var divAnnotation ='<div class="info-source" id ="info-annotation">'+ this.infoAnnotation +' </div>'
      if (this.infoAnnotation ==""){
        divAnnotation ="";
      }

      this.copyHeaderCode = '<link href="https://dynamic.faz.net/red/2023/no-data-infographic-generator/css/app.css" rel="stylesheet"> <div class="info-wrapper">' + divHeadline + divSubline + this.legendHTML + '<div class="first-box" >' + divY
      this.copyFooterCode = divX + divAnnotation + '<div class="info-source">Grafik: '+ this.infoGraphic +' / Quelle: '+ this.infoSource +'</div>  </div>'

      

    }
  
},

  mounted () {

  
  }

}
</script>


<style scoped>
@import './assets/style.css';

.info-wrapper {
    max-width: v-bind(wrapperMaxWidth) 
  }

  .svg-wrapper {
   height: v-bind(wrapperMaxHeight) 
  }

  .y-axis {
    height: v-bind(wrapperMaxHeight)
  }

  .info-color {
    width: v-bind(infoColorWidth)
  }
</style>

---
title: "Primeiro Post"
date: 2017-12-06T19:49:39-03:00
draft: false
---
<script src="https://d3js.org/d3.v4.min.js"></script>

<div class="container">
    <style>
     .chart rect {
          fill: steelblue;
    }

 </style>
    <div class="row">
      <h2>Teste</h2>
    </div>
    <div class="row mychart" id="chart">
    </div>
  </div>

<script type="text/javascript">
    var alturaSVG = 500,
        larguraSVG = 1750;
      function desenhaVis(dados) {  

      }
    
    d3.csv('../dados/dados.csv', function(dados) {
        desenhaVis(dados);
    });
 </script>

</div>

---
title: "Quantidade de veiculos em três principais pontos no entorno do Açude Velho"
date: 2017-12-09T12:50:20-03:00
draft: false
---


<script src="https://d3js.org/d3.v4.min.js"></script>
<style>

.arc text {
  font: 10px sans-serif;
  text-anchor: middle;
}

.arc path {
  stroke: #fff;
}

</style>
<div class="container">
    <div class="row">
      <h2>Quantidade de veiculos em três principais pontos no entorno do Açude Velho:</h2>
    </div>
    <svg width="960" height="500"></svg>


<script type="text/javascript"></script>
<script>

var svg = d3.select("svg"),
    width = +svg.attr("width"),
    height = +svg.attr("height"),
    radius = Math.min(width, height) / 2,
    g = svg.append("g").attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");

var color = ["#3366CC", "#DC3912", "#7b6888", "#6b486b", "#a05d56", "#d0743c", "#ff8c00"];

var pie = d3.pie()
    .sort(null)
    .value(function(d) { return d.valor; });

var path = d3.arc()
    .outerRadius(radius - 10)
    .innerRadius(0);

var label = d3.arc()
    .outerRadius(radius - 40)
    .innerRadius(radius - 40);

d3.csv("../dados/dados.csv", function(d) {
  d.valor = +d.valor;
  return d;
}, function(error, data) {
  if (error) throw error;

  var dados = []
  
  dados.push({"local": "Frente do Bob's", "valor": d3.sum(data.filter((d) => d.local === "bobs"), (d, i) => d.total_motorizados) })
  dados.push({"local": "Monumento do Sesquicentenário", "valor": d3.sum(data.filter((d) => d.local === "burrinhos"), (d, i) => d.total_motorizados) })
  dados.push({"local": "Jackson do Pandeiro", "valor": d3.sum(data.filter((d) => d.local === "jackson"), (d, i) => d.total_motorizados) })
  var arc = g.selectAll(".arc")
    .data(pie(dados))
    .enter().append("g")
      .attr("class", "arc");

  arc.append("path")
      .attr("d", path)
      .attr("fill", function(d, i) { return color[i]; });

  arc.append("text")
      .attr("transform", function(d) { return "translate(" + label.centroid(d) + ")"; })
      .attr("dy", "0.35em")
      .text(function(d, i) { return dados[i].local; });
});

</script>

</div>
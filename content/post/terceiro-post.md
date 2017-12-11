---
title: "Comparação entre pedestres e carros em cada ponto estabelecido"
date: 2017-12-10T21:14:19-03:00
draft: true
---

<script src="https://d3js.org/d3.v4.min.js"></script>

<div class="container">
    <div class="row">
      <h2>Comparação entre pedestres e carros em cada ponto estabelecido:</h2>
    </div>
    <div class="row mychart" id="chart">
    </div>
  </div>

<script type="text/javascript">
    "use strict"
    var alturaSVG = 500,
        larguraSVG = 960;
    function desenhaVis(dados) {
        var cx_apoio = [1,2,3,4,5,6]
        var info_apoio = []
        info_apoio.push({"local": "Frente do Bob's", "valor_carros": d3.sum(dados.filter((d) => d.local === "bobs"), (d, i) => d.carros),
        "valor_pedestres": d3.sum(dados.filter((d) => d.local === "bobs"), (d, i) => d.total_pedestres)})

        info_apoio.push({"local": "Monumento do Sesquicentenário", "valor_carros": d3.sum(dados.filter((d) => d.local === "burrinhos"), (d, i) => d.carros),
        "valor_pedestres": d3.sum(dados.filter((d) => d.local === "burrinhos"), (d, i) => d.total_pedestres)})

        info_apoio.push({"local": "Jackson do Pandeiro", "valor_carros": d3.sum(dados.filter((d) => d.local === "jackson"), (d, i) => d.total_motorizados),
        "valor_pedestres": d3.sum(dados.filter((d) => d.local === "jackson"), (d, i) => d.total_pedestres)})

        console.log(info_apoio)
        
          var grafico = d3.select('#chart') // cria elemento <svg> com um <g> dentro
                            .append('svg')
                              .attr('width', larguraSVG)
                              .attr('height', alturaSVG);
           var grupo = grafico.selectAll('g')
                   .data(info_apoio)
                   .enter()
                   .append('g');
         grupo.append('circle')
            .attr("cx", function(d, i) { 
                return cx_apoio[i] * 250; })
            .attr("cy", 250)
            .attr("r", function(d) { return d.valor_carros * 0.004; })
            .style("fill", "goldenrod");
          grupo.append('circle')
             .attr("cx", function(d, i) { return (cx_apoio[i]) * 250; })
             .attr("cy", 250)
             .attr("r", function(d) { return d.valor_pedestres * 0.004; })
             .style("fill", "steelblue");
        grupo.append('text')
             .text(function(d){
                return d.local;
             })
             .attr("x", function(d,i) { return (cx_apoio[i]) * 250 - 8; }) //Localização de onde o número ficará na barrano eixo X
             .attr("y", 250);
    }
    d3.csv('../dados/dados.csv', function(dados) {
      desenhaVis(dados);
    });
 </script>

</div>
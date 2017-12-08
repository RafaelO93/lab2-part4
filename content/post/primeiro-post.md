---
title: "Primeiro Post"
date: 2017-12-06T19:49:39-03:00
draft: false
---
<script src="https://d3js.org/d3.v4.min.js"></script>

<div class="container">
    <style>
     #chart rect {
          fill: steelblue;
    }
   

</style>
    <div class="row mychart" id="chart">
</div>
</div>

<script type="text/javascript">
    var alturaSVG = 400,
        larguraSVG = 600;

    var	margin = {top: 10, right: 20, bottom:30, left: 45},
          larguraVis = larguraSVG - margin.left - margin.right,
          alturaVis = alturaSVG - margin.top - margin.bottom;


    function desenhaVis(data) {
        //criando o "container"/"esqueleto" do gráfico
        var grafico = d3.select('#chart')
            .append("svg") 
                .attr('width', larguraVis + margin.left + margin.right)
                .attr('height', alturaVis + margin.top + margin.bottom)
            .append('g')
                .attr('transform', 'translate(' +  margin.left + ',' + margin.top + ')');
        //escalas
        var x = d3.scaleBand().domain(data.filter((d) =>
            (d.horario_inicial <= "13:00" && d.horario_inicial >= "11:30")||
            (d.horario_inicial <= "19:00" && d.horario_inicial >="17:30"))
            .map((data, indice) => data.horario_inicial))
            .range([0, larguraVis]).padding(0.1);

        var y = d3.scaleLinear().domain([0, 1300]).range([alturaVis, 0]);

        //dados mostrados
        grafico.selectAll('g')
            .data(data)
            .enter()
            .append('rect')
                .attr('x', d => x(d.horario_inicial))   
                .attr('width', x.bandwidth()) 
                .attr('y', d => y(d.total_motorizados))
                .attr('height', (d) => alturaVis - y(d.total_motorizados));

        //eixos
        grafico.append("g")
            .attr("class", "x axis")
            .attr("transform", "translate(0," + alturaVis + ")")
            .call(d3.axisBottom(x)); 
        grafico.append('g')
            .attr('transform', 'translate(0,0)')
            .call(d3.axisLeft(y));  
        grafico.append("text")
            .attr("transform", "translate(-30," + (alturaVis + margin.top)/2 + ") rotate(-90)")
            .text("Quantidade de carros")
      }

    d3.csv('../dados/dados.csv', function(data) {
        desenhaVis(data);
    });
 </script>

</div>

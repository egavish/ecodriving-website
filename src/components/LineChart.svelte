<script>
    import { scaleLinear } from "d3-scale";
    import Tooltip from "./Tooltip.svelte";
    export let chartWidth;
    export let chartHeight;
    const paddings = {
      top: 50,
      left: 50,
      right: 50,
      bottom: 50,
    };
    export let chart;
    export let data;
    export let xVar;
    export let yVars;
    let xScale = scaleLinear()
        .range([paddings.left, chartWidth - paddings.right]);
    let yScale = scaleLinear()
        .range([chartHeight - paddings.bottom, paddings.top]);
    if (chart === true){
    xScale = scaleLinear()
    .domain([0, Math.max(...data.map((d) => d[xVar])),])
    .range([paddings.left, chartWidth - paddings.right]);
    yScale = scaleLinear()
    .domain([Math.min(...data.map((d) => Math.min(...yVars.map((yVar) => d[yVar])))), Math.max(...data.map((d) => Math.max(...yVars.map((yVar) => d[yVar])))),])
    .range([chartHeight - paddings.bottom, paddings.top])
    .nice(10);
    }
    const idContainer = 'svg-container-' + Math.random() * 1000000
    let mousePosition = { x: null, y: null }
    function followMouse(event) {
      const svg = document.getElementById(idContainer)
      if (svg === null) return
      const dim = svg.getBoundingClientRect()
      const positionInSVG = 
      { x: event.clientX - dim.left, y: event.clientY - dim.top }
      mousePosition =
        positionInSVG.x > paddings.left &&
        positionInSVG.x < chartWidth - paddings.right &&
        positionInSVG.y > paddings.top &&
        positionInSVG.y < chartHeight - paddings.bottom
          ? { x: positionInSVG.x, y: positionInSVG.y }
          : { x: null, y: null }
    }
    function removePointer() {
      mousePosition = { x: null, y: null }
    }
    function computeSelectedXValue(value) {
      return data.filter((d) => xScale(d[xVar]) >= value)[0][xVar]
    }

</script>

<svg width={chartWidth} height={chartHeight} on:mousemove={followMouse}
on:mouseleave={removePointer}
id={idContainer}
style="background-color: white;">
  
     <g>
       <line
         x1={paddings.left}
         x2={chartWidth - paddings.right}
         y1={chartHeight - paddings.bottom}
         y2={chartHeight - paddings.bottom}
         stroke="black"
         stroke-width="2"
       />
       <line
         x1={paddings.left}
         x2={paddings.left}
         y1={paddings.top}
         y2={chartHeight - paddings.bottom}
         stroke="black"
         stroke-width="2"
       />
       <text x={chartWidth/2 - paddings.right} y={chartHeight - 10}>% Adoption Rate</text>
       <text transform={`translate(${30},${chartHeight/2 + paddings.top}) rotate(-90)`}>% Reduction From Baseline</text>
       <text x={paddings.left} y={20}>This reduction in emissions is the equivalent of removing __ cars from the road. </text>
       <g>
        {#if chart}
        {#each data as datum, i}
          {#each yVars as yVar}
            {#if i != data.length - 1}
              <line
                x1={xScale(data[i][xVar])}
                x2={xScale(data[i + 1][xVar])}
                y1={yScale(data[i][yVar])}
                y2={yScale(data[i + 1][yVar])}
                stroke="black"
                stroke-width="2"
              />
           {/if}
          {/each}
        {/each}
        {/if}
      </g>
      </g>
    {#if mousePosition.x !== null}
      <g
        transform=
          "translate({xScale(computeSelectedXValue(mousePosition.x))} 0)">
        <line
          x1="0"
          x2="0"
          y1={paddings.top}
          y2={chartHeight - paddings.bottom - 2}
          stroke="black"
          stroke-width="1"
        />
        {#each yVars as yVar}
          <circle
            cx={0}
            cy={yScale(
               data.find(
                 (d) => d[xVar] === computeSelectedXValue(mousePosition.x)
                 )[yVar]
               )}
            r="3"
          />
        {/each}
      </g>
      {/if}
      {#if mousePosition.x !== null}
        <Tooltip
          labels={yVars}
          values={data.find(
            (d) => d[xVar] === computeSelectedXValue(mousePosition.x))}
          x={mousePosition.x + 180 > chartWidth
            ? mousePosition.x - 195
            : mousePosition.x + 15}
          y={Math.max(0, mousePosition.y - (yVars.length + 2) * 25)}
          backgroundColor={"black"}
          opacity="0.5"
          textColor={"white"}
          title={"Adoption Rate: " + computeSelectedXValue(mousePosition.x)}
          width="180"
          adaptTexts={false}
        />
      {/if}
    </svg>
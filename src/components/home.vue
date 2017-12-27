/* eslint-disable */

<template>
  <div class="container">
  	<div id="plot"></div>
  </div>
</template>

<script>

export default {

	name: 'home',
  
	methods:{

		generateMesh() {

		    const xDomain = [-5, 5];
		    const yDomain = [-5, 5];
		    const step = 1;

		    const a = 1;
		    const b = 1;
		    let xData = [];
		    let yData = [];
		    let zData = [];

		    for (let x = xDomain[0]; x <= xDomain[1]; x = x + step) {
		     	for (let y = yDomain[0]; y <= yDomain[1]; y = y + step) {
		    		xData.push(x);
		     		yData.push(y);
     				zData.push(a * x * x + b * y * y);
		     	}
		    }

		    return {xData, yData, zData};
		}
	},

	mounted() {

		const mesh = this.generateMesh();

    	let data = [{
    		x: mesh.xData,
    		y: mesh.yData,
			z: mesh.zData,
			type: 'mesh3d',
			opacity:0.8,
      		color:'rgb(100,200,200)',
		}];

		let layout = {
			title: 'paraboloid',
			autosize: false,
			width: 900,
			height: 700,
			margin: {
				l: 50,
				r: 50,
				b: 50,
				t: 50
			}
		};

	    Plotly.newPlot('plot', data, layout);
	}
};
</script>

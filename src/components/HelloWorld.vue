/* eslint-disable */
<template>
  <div class="container">
  	<div id="plot"></div>
  </div>
</template>

<script>

export default {

	name: 'HelloWorld',
  
	methods:{
		unpack(rows, key) {
			return rows.map(
				(row) => { 
					return row[key]; 
				});
		},

		generateZAxisData(rows) {
			let zData=[ ];

		    // for(let i=0;i<24;i++) {
		    // 	zData.push(this.unpack(rows, i));
		    // }

		    const xDomain = [-5, 5];
		    const yDomain = [-5, 5];
		    const step = 1;

		    for (let x = xDomain[0]; x <= xDomain[1]; x = x + step) {
		     	for (let y = yDomain[0]; y <= yDomain[1]; y = y + step) {
		     		console.log(x,y)
		     	}
		     } 
debugger
		    return zData;
		}
	},

	mounted() {
		const dataFileUrl = 'https://raw.githubusercontent.com/plotly/datasets/master/api_docs/mt_bruno_elevation.csv';

		Plotly.d3.csv(dataFileUrl, (err, rows) => {
		    let data = [{
				z: this.generateZAxisData(rows),
				type: 'surface'
			}];
		      
		    console.table(data[0].z)
		    let layout = {
				title: 'paraboloid',
				autosize: false,
				width: 800,
				height: 800,
				margin: {
					l: 75,
					r: 75,
					b: 75,
					t: 100,
				}
		    };

		    Plotly.newPlot('plot', data, layout);
		});
	}
};
</script>

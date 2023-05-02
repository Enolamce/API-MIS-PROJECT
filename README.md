# API-MIS-PROJECT
The following API fetches data from NY CITY public database and shows on what day were the highest death due to covid 


THIS IS THE CODE 
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js"></script>
	<style> .btn{border:1px solid black; padding:5px;display:inline-block} </style>
	<style>
		body {
		  background-color: #f1f1f1;
		}
		.container {
		  background-color: #ffffff;
		  border-radius: 10px;
		  padding: 20px;
		  margin-top: 20px;
		}
		h1 {
		  text-align: center;
		}
		.btn{
		  border: 1px solid black;
		  padding: 5px;
		  display: inline-block;
		}
	  </style>
</head>
<body>
	<div class="container">
		<h2>COVID-19 highest Death Count in NEW YORK CITY</h2>
		<p>The following API shows what date between 2020-2022 had the highest deaths due to COVID</p>
		<form>
			<input type="button" value="Go" id="btn_1">
		</form>
		<br><br><br>
		<div id="output"></div>
	</div>
</body>
<script>

function getTheData(){
	console.log("Here we go get the data...");
		$.getJSON('https://data.cityofnewyork.us/resource/rc75-m7u3.json', function(result) {
        console.log(result);

		 let newdata =[];
		for (let i = 0; i < result.length; i++) {
            let item = [];
			item[1] = result[i]['date_of_interest'].split('T')[0];
            item[0] = (result[i]['death_count']);
           	// console.log(item[0] + item[1]) 
            
			newdata[i] = item
           
			}
			console.log("This is the new data pulled from the array")
			console.log(newdata)
		

		 newdata.sort(function(pos1,pos2){return pos2[0] - pos1[0]});
			console.log(newdata)

			plotTheChart(newdata)

		})
		
	}
		function plotTheChart(data){

			let imageurl = "https://image-charts.com/chart?"
			imageurl = imageurl + "chco=ff5555|e7a4e4|b2dffb|ffc55c|bbc55c&"
			imageurl = imageurl + "chd=t:" + data[0][0] + "," + data[1][0] + "," + data[2][0] + "," + data[3][0]+ "," + data[4][0] + "&"
			imageurl = imageurl + "chds=0," + data[0][0] + "&"
			imageurl = imageurl + "chs=700x700&"
			imageurl = imageurl + "cht=bvs&"
			imageurl = imageurl + "chxl=1:|" + data[0][1] + "|" +  data[1][1] + "|" +  data[2][1] + "|" +  data[3][1] + "|" +  data[4][1] + "&"
			imageurl = imageurl + "chxt=y,x";
		
	
			console.log(imageurl);

			$("#output").html("<img src='" + imageurl + "'>"); 
			
		}


//click event handlers

$('#btn_1').click(function(){
	getTheData();
})

</script>
</html>

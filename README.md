
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>表格的行属性</title>
	<style>
		input {
	        /*border: 0; */
	       border: 1px red; 
	        outline: none;
	        background-color: rgba(0,0,0,0);
	        width: 90px;
	 		}
	 	input::-webkit-outer-spin-button,
		input::-webkit-inner-spin-button {
		    -webkit-appearance: none !important;
		    margin: 0;
		}
	 	table {  
            border-collapse: collapse; 
            margin: 0px auto;
            width: 100%; 
        }	
        .jisuan{
        	margin: 20px;
        	margin-right: 50px;
        	float: right;
        }
        body{
        	width: 1300px;
        }
        img{
        	width: 180px;
        	height: 80px;
        	
        }
	</style>
<script>  
	var cars = new Array(3);
	let oot=0;
	var arr1 = new Array(13);
	var arr2 = new Array(13);
	arr1[0]=0;
	arr2[0]=0;
	let ii=0;
	let aa=0;
	let kk;
	let c;
function calculateAverages() {  
    // 获取表格中所有行（除了表头）  
    const rows = document.querySelectorAll('.table1 tr:not(:first-child)');  
  
    // 遍历每一行  
    rows.forEach(row => {  
        let sum = 0;  
        let count = 0;  
  
        // 遍历第二列到第七列的单元格  
        for (let i = 1; i < 7; i++) {  
            let input = row.cells[i].querySelector('input');  
            if (input && !isNaN(input.valueAsNumber)) {  
                sum += input.valueAsNumber;  
                count++;  
            }  
        }  
  
        // 如果有有效数据，则计算平均值并设置到第八列  
        if (count > 0) {  
            let averageCell = row.cells[7];  
            let averageInput = averageCell.querySelector('input') || document.createElement('input');  
            averageInput.type = 'text';  
            averageInput.value = (sum / count).toFixed(6);  
            cars[oot]=(sum / count).toFixed(6);
            oot=oot+1;
            
            
            averageInput.readOnly = true; // 设置为只读，避免用户修改  
            if (!averageCell.firstChild) {  
                averageCell.appendChild(averageInput);  
            } else {  
                averageCell.replaceChild(averageInput, averageCell.firstChild);  
            }  
        } else {  
            // 如果没有有效数据，则清空第八列的输入（如果存在）  
            let averageCell = row.cells[7];  
            if (averageCell.firstChild) {  
                averageCell.removeChild(averageCell.firstChild);  
            }  
        }  
    });  
}  

function calculateDifferences() {  
  
    const row2Cells = document.querySelectorAll('.table2 tr:nth-child(2) td:not(:first-child)');  
    const row3Cells = document.querySelectorAll('.table2 tr:nth-child(3) td:not(:first-child)');  
  	const row4Cells = document.querySelectorAll('.table2 tr:nth-child(4) td:not(:first-child)');  
    const row5Cells = document.querySelectorAll('.table2 tr:nth-child(5) td:not(:first-child)');
 // ii=0
    row2Cells.forEach((cell, index) => {  
        // 获取输入值  
        const inputValue = cell.querySelector('input').valueAsNumber;  
  
        // 如果不是第二列，则计算差值  
        if (index > 0) {  
            // 获取前一列的输入值  
            const prevInputValue = row2Cells[index - 1].querySelector('input').valueAsNumber;  
            // 计算差值  
            const difference = inputValue - prevInputValue;  
            // 将差值设置到第三行的对应单元格中  
            row4Cells[index].querySelector('input').value = difference; 
            ii=ii+1;
            arr1[ii]=difference;
        } else {  
            // 如果是第二列，则第三行对应单元格设为0  
            row4Cells[index].querySelector('input').value = 0;  
        }  
    });  
 //aa=0   
    row3Cells.forEach((cell, index) => {  
        // 获取输入值  
        const inputValue = cell.querySelector('input').valueAsNumber;  
  
        // 如果不是第二列，则计算差值  
        if (index > 0) {  
            // 获取前一列的输入值  
            const prevInputValue = row3Cells[index - 1].querySelector('input').valueAsNumber;  
            // 计算差值  
            const difference = inputValue - prevInputValue;  
            // 将差值设置到第三行的对应单元格中  
            row5Cells[index].querySelector('input').value = difference; 
            aa=aa+1;
            arr2[aa]=difference;
        } else {  
            // 如果是第二列，则第三行对应单元格设为0  
            row5Cells[index].querySelector('input').value = 0;  
        }  
    });
}
function getColumnData() {  
 	var a=cars[0];
	var b=cars[1];
	c=cars[2];
	
	console.log("a:", a);  
    console.log("b:", b);  
    console.log("c:", c);
    var wa=2*b/a;
    document.getElementById("demo").innerHTML = wa;
   
}  

function getColumnData2() {  
//	let arr1 = document.querySelectorAll('.table2 tr:nth-child(4) td:not(:first-child)'); // 第四行  
//	let arr2 = document.querySelectorAll('.table2 tr:nth-child(5) td:not(:first-child)'); // 第五行  
	  
	let sumFirstSeven1 = arr1.slice(0, 7).reduce((acc, curr) => acc + curr, 0);
	let sumLastSix1 = arr1.slice(7, 13).reduce((acc, curr) => acc + curr, 0); 
	let result1 = sumLastSix1 - sumFirstSeven1; 
	
	let sumFirstSeven2 = arr2.slice(0, 7).reduce((acc, curr) => acc + curr, 0);
	let sumLastSix2 = arr2.slice(7, 13).reduce((acc, curr) => acc + curr, 0); 
	let result2 = sumLastSix2 - sumFirstSeven2; 
	
	console.log(arr1); // 输出第四行的数据  
	console.log(arr2); // 输出第五行的数据
	kk=result1/result2;
    document.getElementById("demo2").innerHTML = kk;
   
} 

function getColumnData3() {  
	
	let aab=kk/c;
    document.getElementById("demo3").innerHTML = aab;
   
}
</script>  
</head>  
<body>  
  
<h2>平均值计算表格</h2>  
<table border="2" align="center" class="table1">  
    <tr>  
        <th>  </th>  
        <th>1</th>  
        <th>2</th>  
        <th>3</th>  
        <th>4</th>  
        <th>5</th>  
        <th>6</th>  
        <th>平均值</th>  
    </tr>  
    <tr>  
        <td style="font-size:20px;">d</td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="text" readonly></td>  
    </tr>  
    <tr>  
        <td style="font-size:20px;">D</td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="text" readonly></td>  
    </tr>  
    <tr>  
        <td style="font-size:20px;">L</td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="number"></td>  
        <td><input type="text" readonly></td>  
    </tr>  
</table>  
<button onclick="calculateAverages()" class="jisuan">计算平均值</button>  
  
  <div class="divv">
  	<h2>13次测量的数据</h2>  
	<table border="2" align="center" class="table2">  
	    <tr>  
	        <th></th>  
	        <th>1</th>  
	        <th>2</th>  
	        <th>3</th>  
	        <th>4</th>  
	        <th>5</th>  
	        <th>6</th>  
	        <th>7</th>
	        <th>8</th>  
	        <th>9</th>  
	        <th>10</th>  
	        <th>11</th>  
	        <th>12</th>  
	        <th>13</th>  
	    </tr>  
	    <tr>  
	        <td style="font-size:20px;">n</td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	    </tr>  
	    <tr>  
	        <td style="font-size:20px;">t</td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>
	    </tr>  
	    <tr>  
	        <td style="font-size:20px;">▲n</td>  
	        <td><input type="number" readonly value="0"></td> <!-- 第三行第二列直接设为0且只读 -->  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>
	    </tr>
	    <tr>  
	        <td style="font-size:20px;">▲t</td>  
	        <td><input type="number" readonly value="0"></td> <!-- 第三行第二列直接设为0且只读 -->  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td> 
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>  
	        <td><input type="number"></td>
	    </tr>  
	</table>  
	 
	<button onclick="calculateDifferences()" class="jisuan">计算差值</button>  

  </div>
  
  <div class="result">
  	<p>-----------------------------------------</p>
  	<img src="img/3.png" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  	<img src="img/1.png" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  	<img src="img/2.png" />
  	<p> M= <span id="demo">?</span> .
  		<button onclick="getColumnData()">显示答案</button>  
  	</p>
  	
  	<p> K= <span id="demo2"> ?</span> .
  		<button onclick="getColumnData2()">显示答案</button>
  	</p>
  	
  	<p> α= <span id="demo3"> ?</span> .
  		<button onclick="getColumnData3()">显示答案</button>
  	</p>
  </div>
</body>  
</html>

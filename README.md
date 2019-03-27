# Pixel-Art-Maker
// Select color input
// Select size input

// When size is submitted by the user, call makeGrid()

// Define variables for DOM elements
let sizePicker = document.getElementById("sizePicker");
let pixelCanvas = document.getElementById("pixelCanvas");
let inputHeight = document.getElementById("inputHeight");
let inputWidth = document.getElementById("inputWidth");
let colorPicker = document.getElementById("colorPicker");

// Click event listener function
function pixelClick(evt){
	// set selected color value as the background color of clicked cell
	evt.target.style.backgroundColor = colorPicker.value;
}

function makeGrid(evt) {
	// Your code goes here!
	// Disable default behavior of onsubmit event
	evt.preventDefault();

	

	// reset grid: with while loops
	while(pixelCanvas.hasChildNodes()){
		let row = pixelCanvas.firstChild;
		while(row.hasChildNodes()){
			// remove every cell in the row
			let cell = row.firstChild;
			// remove event listener
			cell.removeEventListener("click", pixelClick);
			// remove cell itself
			row.removeChild(cell);
		}
		// remove every roe in the grid
		pixelCanvas.removeChild(row);
	}

	// create new grid with specified size
	for(let row = 0; row < inputHeight.value; row++){
		// Create TR (table row) element for every row in thr grid
		let tr = document.createElement("tr");
		for(let col = 0; col < inputWidth.value; col++){
			// create TD (table cell) element for every column in the grid
			let td = document.createElement("td");
			// attach event listener function (pixelClick) to cell's onclick event
			td.addEventListener("click", pixelClick);
			// append new cell to the row
			tr.appendChild(td);
		}
		// append new row to the grid
		pixelCanvas.appendChild(tr);
	}
}

// sizePicker.onsubmit =  makeGrid;
sizePicker.addEventListener("submit", makeGrid);

# Studio-Project-6

https://amiarr.github.io/Studio-Project-6/

Technical Documentation 

Brush 

I wanted to create an interactive canvas with brushes on P5JS, so I used a YouTube tutorial, https://www.youtube.com/watch?v=tCvvPDJB274, to learn how to create a paintbrush using ellipses. The initial function that I used was - 

function draw () {
 fill (205, 105, 180);
 noStroke ();
 ellipse(moouseX, mouseY, 30);
}


function  mousePressed () {
background (0);
 }

Which I directly took from the Youtube video. I also wanted to make the brush have a glowing effect, as that is something I had previously done in Workshop 7 (https://github.com/AmiaRR/Workshop-7), and used shadowBlur to achieve that.

Sliders 
I wanted to be able to control the colour of the paintbrush, and decided to do this using the sliders I learnt about in Workshop 4 (https://github.com/AmiaRR/Workshop-4). I also included another slider to be able to control the size of the brush. I realised once I had made the sliders that the paint would touch the canvas when it was being clicked, so I added drawSliderBox and drawSizeBox to achieve this. I also wanted the colour being selected to be visible to the user, so the function getSelectedColor was used to create the gradient of the box. I used ChatGPT to help create these slider functions, by asking ChatGPT on how I would use a slider to control the colour and size of the brush I had made previously, and included this code in my sketch, the same with getSelectedColour. 

// Sliders 
function drawColorSlider() {
 colorMode(HSB, 255, 100, 100);
 fill(50);
 stroke(360);
 rect(sliderBox.x, sliderBox.y, sliderBox.w, sliderBox.h);


  for (let i = 0; i < sliderBox.w; i++) {
   let hueValue = map(i, 0, sliderBox.w - 1, 0, 255);
   stroke(hueValue, 100, 100);
   line(sliderBox.x + i, sliderBox.y, sliderBox.x + i, sliderBox.y + sliderBox.h);
 }
}
function getSelectedColor() {
 let hueValue = map(sliderValue, 0, sliderBox.w - 1, 0, 255);
 return color(hueValue, 100, 100);
}




function mousePressed() {
 if (mouseY > sliderBox.y && mouseY < sliderBox.y + sliderBox.h &&
     mouseX > sliderBox.x && mouseX < sliderBox.x + sliderBox.w) {
   sliderValue = mouseX - sliderBox.x;
   brushColor = getSelectedColor();
 }
}
function drawSizeSlider() {
 fill(50);
 stroke(255);
 rect(sizeBox.x, sizeBox.y, sizeBox.w, sizeBox.h);
 fill(255);
 noStroke();
 textSize(14);
 textAlign(CENTER, CENTER);
 text('', sizeBox.x + sizeBox.w / 2, sizeBox.y + sizeBox.h / 2);
}
// Slider boxes 
function drawSliderBox() {
 colorMode(HSB);
 for (let i = 0; i < sliderBox.w; i++) {
   let hueValue = map(i, 0, sliderBox.w, 0, 360);
   stroke(hueValue, 100, 100);
   line(sliderBox.x + i, sliderBox.y, sliderBox.x + i, sliderBox.y + sliderBox.h);
 }
 noFill();
 stroke(255);
 rect(sliderBox.x, sliderBox.y, sliderBox.w, sliderBox.h);
 colorMode(RGB);
}
  noFill();
 stroke(360);
 rect(sliderBox.x, sliderBox.y, sliderBox.w, sliderBox.h);




function drawSizeBox() {
 fill(50);
 stroke(255);
 rect(sizeBox.x, sizeBox.y, sizeBox.w, sizeBox.h);
}



Saving Tiles/Clear Canvas
I used deleteButton and saveButton to be able to save the sketch as a ‘tile’and clear the canvas, which I prompted ChatGPT to help implement these functions into my code. For the save button, I gave a very specific prompt to ChatGPT, stating that I wanted to save the sketch as a square when save was pressed, and the tiles should go in rows of three, and the canvas should go beneath the tiles, so that the user could scroll down and still use the canvas, which worked. Originally the ‘Save Drawing’ button saved the sketch as a png to the computer, however I wanted the sketches to turn into a collection of tiles, kind of similar to how My Boyfriend Came Back From the War and Glyphtti both have interactive boxes, which is why I changed the purpose of the save button. Like with the sliders, I added boxes to the buttons, and experimented with the size and placement of these boxes and buttons. Unfortunately these boxes didn’t prevent paint from the top of the canvas being visible on the saved canvas, so one of the last things I did to my code was add a black box the width of the canvas, so that none of the paint could touch the sliders or buttons. 


function saveTile() {
 let tile = createGraphics(tileSize, tileSize);
 tile.colorMode(HSB);
 tile.background(0);
 if (img) {
   tile.image(img, 0, 0, tileSize, tileSize);
 }
 tile.image(drawingLayer, 0, 0, tileSize, tileSize);
 tiles.push(tile);
 tileRows = ceil(tiles.length / tilesPerRow);
 tileAreaHeight = (tileSize + tileSpacing) * tileRows + 20;
 updateCanvasPosition();
}


function drawTiles() {
 let xOffset = 10;
 let yOffset = 150;
 for (let i = 0; i < tiles.length; i++) {
   let row = floor(i / tilesPerRow);
   let col = i % tilesPerRow;
   let x = xOffset + col * (tileSize + tileSpacing);
   let y = yOffset + row * (tileSize + tileSpacing);
   fill(0);
   rect(x, y, tileSize, tileSize);
   image(tiles[i], x, y, tileSize, tileSize);
 }
}


function clearCanvas() {
 drawingLayer.clear();
 drawingLayer.background(0);
}

saveButton = createButton('Save Drawing');
 saveButton.position(saveBox.x + 10, saveBox.y + 10);
 saveButton.mousePressed(saveTile);


 deleteButton = createButton('Clear Canvas');
 deleteButton.position(deleteBox.x + 10, deleteBox.y + 10);
 deleteButton.mousePressed(clearCanvas);

Sound 
I wanted to include sound effects to my paintbrush, as that is a common feature of many drawing tools. I first downloaded a paintbrush sound effect as a wav file from epidemicsound.com, which I labelled paintbrush1.wav and added it to my code. I then asked ChatGPT on how I could make this audio play when the mouse was clicked, and stop when the mouse stopped clicking, and I directly implemented the solution given into my code. This code initially worked well, but as I was adding more functions to my code, it stopped working at some point. Unfortunately I wasn’t coding with volume on, so I wasn’t able to pinpoint when exactly it stopped working, which might have helped me figure out what I did wrong. After seeking further help, I found that I needed to add brushSound.loop(); for it to be able to work. It did work, however it sounded kind of static and not like the audio, I tried using ChatGPT and making another simple brush sound sketch to copy and paste, but unfortunately it still sounded like static. Initially I decided to just turn down the volume really low, so that the audio technically still worked, but the noise wasn’t as noticeable, though when I uploaded this new sketch as a web page, it was noticeably very slower than the last one I made, and would stop working and permanently freeze after a short period of time, as shown in this screenshot. I still kept the GitHub, which shows my attempt at using audio in my sketch, however it is obviously slower than the Github I had made previously, I’m not sure if that is related to the audio or not. Ultimately I decided to leave the audio for the final hand-in, as I wanted to retain the functionality of the rest of the sketch. 
https://amiarr.github.io/Studio-Project-7/

<img width="497" alt="Screenshot 2025-02-18 at 2 40 06 PM" src="https://github.com/user-attachments/assets/2e613538-9215-48c7-89c1-7d68c0b36406" />



function preload() {
 soundFormats('wav');
 brushSound = loadSound('paintbrush1.wav');
 };




function mousePressed() {
 userStartAudio()
 if (mouseY > tileAreaHeight && brushSound) {
   brushSound.loop();
 }
}


function mouseReleased() {
 if (brushSound) {
   brushSound.stop();
 }
}
 


Adding Images  
In formative feedback I was given code to be able to add images to my sketch. I didn’t plan to include images into my sketch, but the function worked and makes the sketch more interactive for the user. Initially the ‘choose file’ button was where the ‘upload tile’ button is in the final piece, and it had a box, but I moved it to the right of the sliders to make space for ‘upload tile.’ 

function handleFile(file) {
 if (file.type === 'image') {
   img = loadImage(file.data, () => {
     drawingLayer.image(img, 0, 0, canvasWidth, canvasHeight);
   });
 }
}

Uploading Tiles 
I had decided that I wanted collaborativeness to be a key link between my sketch and the concept of digital folklore. The most obvious way I could think of to make my sketch collaborative was to have the tiles be able to be uploaded into a publicly accessible collection. I had no idea on how to achieve this and I asked ChatGPT for some potential solutions for this, and ChatGPT offered several solutions including Firebase, Supabass, PostImages, and Google API. Initially none of these options I tried worked. I tried to make a publicly accessible Google Drive and use Google API, following instructions from ChatGPT many times, making several different Drive folders. For some reason, one of my attempts worked, I’m not exactly sure why, I think it might have had to do with not using my university email, but I don’t know. I also prompted ChatGPT asking how I would create a link so that the user would be able to easily find the drive folder. I could improved this code by finding a way to make it so that the user would have a visual confirmation that their tile had been uploaded, because from own experience, not seeing the tile uploaded yet onto the drive could result in spam clicking, and therefore an excessive number of identical tiles being uploaded, and also I’m assuming there's a finite amount of space on a Google Drive folder as well.  

function uploadTile() {
 if (tiles.length === 0) {
   console.log("No tiles to upload!");
   return;
 }


 let tile = tiles[tiles.length - 1];


 tile.elt.toBlob(blob => {
   let formData = new FormData();


   let base64Image = tile.elt.toDataURL("image/png").split(',')[1];


   formData.append("image", base64Image);


   fetch("https://script.google.com/macros/s/AKfycbyIW03hg_wBSZ4cR5QTGC2UbCHk-FrVo05bIivQj0hxltTDib_6yQEg4AFrFasfljY/exec", {
     method: "POST",
     body: formData
   }).then(response => response.text())
     .then(data => {
       console.log("Upload Success:", data);


       alert("Tile uploaded! View collection here: " + data);
     })
     .catch(error => console.error("Upload Failed:", error));
 }, "image/png");
}




Brush Selection 
In the group feedback sessions during the final zoom class, I was given feedback that I should include a selection of different brushes for the user to choose. I wasn't sure what different kinds of brushes I wanted to include, so I watched some youtube videos for ideas, such as https://www.youtube.com/watch?v=olXv8GOfpNw and then experimented with these ideas on the online p5js editor. I ended up deciding I wanted a watercolour brush, a pixel brush (to reference Glyphiti) as well as keeping my original, glowy paint brush which I labelled ‘spray paint.’ I prompted ChatGPT to give me code to include in my sketch. I also used ChatGPT on how I would create 3 clickable buttons for these 3 brushes, I decided to have the buttons vertically placed between the left buttons and the sliders, with a cluster of dots representing spray paint, a semi-transparent circle representing watercolour, and a square to represent the pixels. As I asked ChatGPT for code to help achieve this specific idea, it decided to make the dots for the ‘spray paint’ icon animated, which wasn’t what I had in mind, but I decided to leave it. I also made the icons pink, and purple when pressed, so the user would be able to tell what brush was being used.  	


function drawBrush() {
 if (mouseIsPressed && mouseY > 160) {
   let hueValue = map(colorSlider.value(), 0, sliderBox.w, 0, 360);
   let brushSize = sizeSlider.value();

   fill(hueValue, 100, 100);
   noStroke();

   switch (currentBrush) {
     case 'spray':
       drawSprayBrush(hueValue, brushSize);
       break;
     case 'watercolor':
       drawWatercolorBrush(hueValue, brushSize);
       break;
     case 'pixel':
       drawPixelBrush(hueValue, brushSize);
       break;
   }
 }
}


function drawSprayBrush(hueValue, brushSize) {
 let ctx = drawingLayer.drawingContext;
 ctx.shadowBlur = 15;
 ctx.shadowColor = color(hueValue, 100, 100);

 swirlAngle += 0.1;
 let xOffset = sin(swirlAngle) * 1;
 let yOffset = cos(swirlAngle) * 1;

 drawingLayer.fill(hueValue, 100, 100);
 drawingLayer.noStroke();
 drawingLayer.ellipse(mouseX + xOffset, mouseY - tileAreaHeight + yOffset, brushSize);

 ctx.shadowBlur = 0;
}

function drawWatercolorBrush(hueValue, brushSize) {
 let numParticles = int(random(10, 20));
 for (let i = 0; i < numParticles; i++) {
   let offsetX = random(-5, 5);
   let offsetY = random(-5, 5);
   let size = random(brushSize / 2, brushSize);
   let numParticles = int(random(20, 40));
let alpha = random(5, 15);
   let col = color(hueValue, 100, 100, alpha);
 

   drawingLayer.noStroke();
   drawingLayer.fill(col);
   drawingLayer.ellipse(mouseX + offsetX, mouseY - tileAreaHeight + offsetY, size);
 }
}

function drawPixelBrush(hueValue, brushSize) {
 let gridSize = max(1, floor(brushSize / 3));
 let px = floor(mouseX / gridSize) * gridSize;
 let py = floor((mouseY - tileAreaHeight) / gridSize) * gridSize;

 drawingLayer.noStroke();
 drawingLayer.fill(color(hueValue, 100, 100));
 drawingLayer.rect(px, py, gridSize, gridSize);
}

function setupBrushButtons() {
 let startY = 10;
 let startX = 140;
 let brushTypes = ['spray', 'watercolor', 'pixel'];


 for (let i = 0; i < brushTypes.length; i++) {
   let y = startY + i * (brushIconSize + brushIconSpacing);
   brushButtons.push({
     x: startX,
     y: y,
     type: brushTypes[i]
   });
 }
}


function drawBrushIcons() {
 colorMode(HSB, 360, 100, 100, 100);
 
 fill(0);
 noStroke();
 rect(brushButtons[0].x - 5, brushButtons[0].y - 5, brushIconSize + 10, brushIconSize * 3 + 20);


 for (let i = 0; i < brushButtons.length; i++) {
   let button = brushButtons[i];
   let isSelected = currentBrush === button.type;


  
   let alpha = (i === 1) ? 50 : 100; 


  
   let baseHue = 320;
   let selectedHue = 280;
   let buttonColor = isSelected ? color(selectedHue, 100, 100, alpha) : color(baseHue, 100, 100, alpha);


   fill(buttonColor);
   stroke(0);


   if (i === 0) {
    
     let centerX = button.x + brushIconSize / 2;
     let centerY = button.y + brushIconSize / 2;
    
     for (let j = 0; j < 60; j++) {
       let angle = random(TWO_PI);
       let radius = random(0, brushIconSize / 2);
       let x = centerX + cos(angle) * radius;
       let y = centerY + sin(angle) * radius;
       let dotSize = random(2, 5);
       fill(buttonColor);
       ellipse(x, y, dotSize);
     }
   }
   else if (i === 1) {
    
     let centerX = button.x + brushIconSize / 2;
     let centerY = button.y + brushIconSize / 2;
     let blobSize = brushIconSize * 0.8;


     fill(buttonColor);
     noStroke();
     ellipse(centerX, centerY, blobSize);
   }
   else {
    
     rect(button.x, button.y, brushIconSize, brushIconSize);
   }
 }
}




function mousePressed() {
 for (let button of brushButtons) {
   if (
     mouseX > button.x && mouseX < button.x + brushIconSize &&
     mouseY > button.y && mouseY < button.y + brushIconSize
   ) {
     currentBrush = button.type;
     return;
   }
 }


  drawBrushStroke();
}

<img width="355" alt="Screenshot 2025-02-18 at 2 40 34 PM" src="https://github.com/user-attachments/assets/5439bf17-a712-44b6-88e3-33c1dca5b2bb" />















# Studio-Project-6

https://amiarr.github.io/Studio-Project-6/

**Technical Documentation**

**Brush**

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

**Sliders** 
I wanted to be able to control the colour of the paintbrush, and decided to do this using the sliders I learnt about in Workshop 4 (https://github.com/AmiaRR/Workshop-4). I also included another slider to be able to control the size of the brush. I realised once I had made the sliders that the paint would touch the canvas when it was being clicked, so I added drawSliderBox and drawSizeBox to achieve this. I also wanted the colour being selected to be visible to the user, so the function getSelectedColor was used to create the gradient of the box. I used ChatGPT to help create these slider functions, by asking ChatGPT on how I would use a slider to control the colour and size of the brush I had made previously, and included this code in my sketch, the same with getSelectedColour. 


**Saving Tiles/Clear Canvas**
I used deleteButton and saveButton to be able to save the sketch as a ‘tile’and clear the canvas, which I prompted ChatGPT to help implement these functions into my code. For the save button, I gave a very specific prompt to ChatGPT, stating that I wanted to save the sketch as a square when save was pressed, and the tiles should go in rows of three, and the canvas should go beneath the tiles, so that the user could scroll down and still use the canvas, which worked. Originally the ‘Save Drawing’ button saved the sketch as a png to the computer, however I wanted the sketches to turn into a collection of tiles, kind of similar to how My Boyfriend Came Back From the War and Glyphtti both have interactive boxes, which is why I changed the purpose of the save button. Like with the sliders, I added boxes to the buttons, and experimented with the size and placement of these boxes and buttons. Unfortunately these boxes didn’t prevent paint from the top of the canvas being visible on the saved canvas, so one of the last things I did to my code was add a black box the width of the canvas, so that none of the paint could touch the sliders or buttons. 


**Sound**
I wanted to include sound effects to my paintbrush, as that is a common feature of many drawing tools. I first downloaded a paintbrush sound effect as a wav file from epidemicsound.com, which I labelled paintbrush1.wav and added it to my code. I then asked ChatGPT on how I could make this audio play when the mouse was clicked, and stop when the mouse stopped clicking, and I directly implemented the solution given into my code. This code initially worked well, but as I was adding more functions to my code, it stopped working at some point. Unfortunately I wasn’t coding with volume on, so I wasn’t able to pinpoint when exactly it stopped working, which might have helped me figure out what I did wrong. After seeking further help, I found that I needed to add brushSound.loop(); for it to be able to work. It did work, however it sounded kind of static and not like the audio, I tried using ChatGPT and making another simple brush sound sketch to copy and paste, but unfortunately it still sounded like static. Initially I decided to just turn down the volume really low, so that the audio technically still worked, but the noise wasn’t as noticeable, though when I uploaded this new sketch as a web page, it was noticeably very slower than the last one I made, and would stop working and permanently freeze after a short period of time, as shown in this screenshot. I still kept the GitHub, which shows my attempt at using audio in my sketch, however it is obviously slower than the Github I had made previously, I’m not sure if that is related to the audio or not. Ultimately I decided to leave the audio for the final hand-in, as I wanted to retain the functionality of the rest of the sketch. 
https://amiarr.github.io/Studio-Project-7/

<img width="497" alt="Screenshot 2025-02-18 at 2 40 06 PM" src="https://github.com/user-attachments/assets/2e613538-9215-48c7-89c1-7d68c0b36406" />



**Adding Images**  
In formative feedback I was given code to be able to add images to my sketch. I didn’t plan to include images into my sketch, but the function worked and makes the sketch more interactive for the user. Initially the ‘choose file’ button was where the ‘upload tile’ button is in the final piece, and it had a box, but I moved it to the right of the sliders to make space for ‘upload tile.’ 



**Uploading Tiles** 
I had decided that I wanted collaborativeness to be a key link between my sketch and the concept of digital folklore. The most obvious way I could think of to make my sketch collaborative was to have the tiles be able to be uploaded into a publicly accessible collection. I had no idea on how to achieve this and I asked ChatGPT for some potential solutions for this, and ChatGPT offered several solutions including Firebase, Supabass, PostImages, and Google API. Initially none of these options I tried worked. I tried to make a publicly accessible Google Drive and use Google API, following instructions from ChatGPT many times, making several different Drive folders. For some reason, one of my attempts worked, I’m not exactly sure why, I think it might have had to do with not using my university email, but I don’t know. I also prompted ChatGPT asking how I would create a link so that the user would be able to easily find the drive folder. I could improved this code by finding a way to make it so that the user would have a visual confirmation that their tile had been uploaded, because from own experience, not seeing the tile uploaded yet onto the drive could result in spam clicking, and therefore an excessive number of identical tiles being uploaded, and also I’m assuming there's a finite amount of space on a Google Drive folder as well.  



**Brush Selection** 
In the group feedback sessions during the final zoom class, I was given feedback that I should include a selection of different brushes for the user to choose. I wasn't sure what different kinds of brushes I wanted to include, so I watched some youtube videos for ideas, such as https://www.youtube.com/watch?v=olXv8GOfpNw and then experimented with these ideas on the online p5js editor. I ended up deciding I wanted a watercolour brush, a pixel brush (to reference Glyphiti) as well as keeping my original, glowy paint brush which I labelled ‘spray paint.’ I prompted ChatGPT to give me code to include in my sketch. I also used ChatGPT on how I would create 3 clickable buttons for these 3 brushes, I decided to have the buttons vertically placed between the left buttons and the sliders, with a cluster of dots representing spray paint, a semi-transparent circle representing watercolour, and a square to represent the pixels. As I asked ChatGPT for code to help achieve this specific idea, it decided to make the dots for the ‘spray paint’ icon animated, which wasn’t what I had in mind, but I decided to leave it. I also made the icons pink, and purple when pressed, so the user would be able to tell what brush was being used.  	


<img width="355" alt="Screenshot 2025-02-18 at 2 40 34 PM" src="https://github.com/user-attachments/assets/5439bf17-a712-44b6-88e3-33c1dca5b2bb" />















<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
	<title> Flappy Bird </title>
</head>
<body>

<canvas width="500" height="400" style="border: 1px solid black">
</canvas>

<script>

var c = document.querySelector("canvas");
var cc = c.getContext("2d");

var bgImg = new Image();
bgImg.src = "bg.png";

var pipeImg = new Image();
pipeImg.src = "pipe1.png";

var pipe2Img = new Image();
pipe2Img.src = "pipe2.png";

var birdImg = new Image();
birdImg.src = "bird.png"

var bg = {
	x: 0,
	y: 0
} 

var bird = {
	x: 100,
	y: 150,
	width: birdImg.width,
	height: birdImg.height
} 

var pipe = {
	x: c.width,
	y: Math.floor(Math.random()*(0-100)+0),
	width: pipeImg.width,
	height: pipeImg.height
}

var pipe2 = {
	x: c.width,
	y: Math.floor(Math.random()*(300-250)+250),
	width: pipe2Img.width,
	height: pipe2Img.height
}

score = 0;
hscore = 0;

document.addEventListener("pointerdown",movs);

function movs(e){
	bird.y -= 50;	
}

function update(){
	pipe.x -= 5;
	pipe2.x -= 5;

	bird.y += 5;

	if (pipe.x < -pipe.width){
		pipe.x = c.width;
		pipe.y = Math.floor(Math.random()*(0-100)+0);
	}

	if (pipe2.x < -pipe2.width){
		pipe2.x = c.width;
		pipe2.y = Math.floor(Math.random()*(300-250)+250);
	}

	if(
		bird.x <= (pipe.x+pipe.width)&&
		pipe.x <= (bird.x+bird.width)&&
		bird.y <= (pipe.y+pipe.height)&&
		pipe.y <= (bird.y+bird.height)
	){
		if (hscore <= score){
			hscore = score;
		}
		score = 0;
		bird.x = 100;
		bird.y = 150;
	}

	if(
		bird.x <= (pipe2.x+pipe2.width)&&
		pipe2.x <= (bird.x+bird.width)&&
		bird.y <= (pipe2.y+pipe2.height)&&
		pipe2.y <= (bird.y+bird.height)
	){
		if (hscore <= score){
			hscore = score;
		}		
		score = 0;
		bird.x = 100;
		bird.y = 150;
	}

	if (bird.x == pipe.x){
		score += 1;
	}	

	if (bird.y > c.height){
		bird.x = 100;
		bird.y = 150;
		if (hscore <= score){
			hscore = score;
		}		
		score = 0;
		bird.x = 100;
		bird.y = 150;		
	}

	if (bird.y < 0){
		bird.x = 100;
		bird.y = 150;
		if (hscore <= score){
			hscore = score;
		}		
		score = 0;
		bird.x = 100;
		bird.y = 150;		
	}
}

function render(){
	cc.drawImage(bgImg,bg.x,bg.y);
	cc.drawImage(pipeImg,pipe.x,pipe.y);
	cc.drawImage(pipe2Img,pipe2.x,pipe2.y);	
	cc.drawImage(birdImg,bird.x,bird.y);

	cc.fillStyle = "black";
	cc.font = "25px Aerial";
	cc.fillText("Score: "+score+"  HighScore: "+hscore,30,40);
}

function loop(){
	render();
	update();
}

setInterval(loop,1000/60)

</script>

</body>
</html>

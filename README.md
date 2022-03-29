# tennis_game
Built Tennis Game in HTML 5 Canvas and Javascript

HTML = hypertext markup language, how people from webpages, like designing newspapers or magazines but for the web. All browsers use this to display web pages
For dynamic content like video games, use canvas elements. Black rectangle game is in canvas element then JavaScript in HTML to bring game to live, logic done in JS, JS embedded in our HTML
Need extension because in code your going to full name and type foundations, tags.
Txt will print text, even if html logic is inside it, need to change file type to html
<script>JS logic in here</script>
console.log(“hello world”) = built in command in JS browser, interpreter allows us to add to error logic 
“ “ arguments, semicolon optional
Internet explorer is different than chrome and firefox
IE will only display a console log if the console is already open when code runs. 
If you make error in code, comes up in error log with file name and line #, unfortunately it wont show variable name typos due to how JS works
If code is broken and no errors, check any recently used variables in code for typos
window.onload = as soon as window finishes loading run the code in the {}, we don't want code to run until all code loaded
Canvas element where graphics will be happening
Block for canvas on screen for game, dimensions, id = gameCanvas - will use in JS to display graphics into it
In script, declare 2 variables, canvas and canvasContext
JS doesn't require declaration of global variables, but you should
Canvas = dimensions of display area
canvasContext = graphic info (draw rectangle etc)
Variable = anything we want to hang on to for future reference
fillRect(_, _, _, _) first and 2nd are top and left, 3rd and 4th are bottom and right
White box is drawn later and painting over it - draw order important because it will go in the order you code it, and as you go down will overlap it
We did canvas.width/2 to get center
Add drawings into a function drawEverything()
Function = label and call it anywhere else in code, code inside function doesn't get run if you don't call it
Position changes every time = BallX = horizontal position, x coordinate in ball set to 50, call it in fillRect(). Start at position BallX if you want the position to change every time, make BallX+10, take the value on the right side and put that on the left side. console.log(Ballx) shows ball x value every time 
Show motion every time (basic dynamic animation)  - adding a timer that is going to call drawEverything() at a regular interval. Set interval (drawEverything, 1000), will call it every 1000 seconds. Increased update rate for smoother movement
Move and resize box - it will become paddle - 0,210,10,100 move code into moveEveryhing() add that to setInterval. Add callBoth function, add both to it and call it in setInterval
Writing function inline - can't be called anywhere else
Create variable to support speed changes = BallX adding 5 per frame, var BallSpeedX =5; ballX = ballX + ballSpeedX
Speed+1 = speed at which moving right
Get ball moving to opposite direction = negative value for speed
Speed same after hitting end of screen, size of window = 800 px if ball exceeds 800, lets flip direction of ball, instead of hard code number, add ballSpeedX
Using canvas dimensions, not hardcoding - in if add canvas.width if you change window size later, automatically gets reflected
Bounce ball off left side too = right side - canvas width left side - ball x value is distance from left, if left < 0, negative, we are multiplying -1 withit
Creating function for drawing filled shapes - with params
Making ball circle = begin path() fill in circle there is no arc fill like fillRect, arc -(x, y, radius, angles, radians around circle, true- whether clockwise or counterclockwise
Dealing with circles center, radius, and color = add into function like color in rectangle
Move and bounce ball vertically = add ballY and ballSpeedY in drawEveything() replace 150 with BallY
Paddle to move where mouse is = defined labeled value for paddle position and size, const = cant be changed when game is playing
Find mouse position relative to game canvas = event first every time mouse moves hand function coordination, it receives part of event
getBoundaryClientRect - area of black rectangle
Document element = html page 
Mouse x and y = getting position of x and y where is canvas element how far we changed browser
Set paddle position value whenever mouse moves = to add input in JS, use AddEventListener, different parameters you can enter liek mouse down key press, etc. getting evt from mouse info, adding as param in calculateMousePos() thats returning x and y coordinates, getting y and updating paddle 1Y
Use paddle position var in paddles draw code = align center on mouse y = position - PADDLE_HEIGHT / 2 (half o paddle height - center)
Good thing about setting constant and using /2 if i come back and change it to 250, no other changes needed. 
Write function that can reset the wall = ballReset() width / 2 add it in BallX < 0 because if it -num will go off screen, call reset there, to flip direction add -
Bounce ball if it gets blocked by left paddle = if below top of paddle and above bottom, or paddle top and height as its already crossing left side, it will flip ball horizontal speed cuz its going to bounce off that paddle otherwise ball reset and also test with edges
Draw right side paddle = 10 px thick 800 px wide canvas so 790, so we can set it up like canvas.width - 10
Create value label for paddle thickness - const PADDLE_THICKNESS = 10; we can use for later won't know what 10, so replace it
Temp use mouse for testing right paddle - change logic in mouse event padd2Y
Reset ball if it goes past right side - do same logic as left paddle but Paddle2Y
Want right paddle to work on its own = get right paddle chasing balls vertical position, make function computerMovement and call t in moveEverything function, is paddle fro other player above the ball, if so +6 else below ball -6
Change to A+=B form, quicker and compact, 
Add A line up right paddles center not top of bottom = add var Paddle2Y (top of paddle) + PADDLE_HEIGHT/2 (half of height)
Stop right paddle from shaking = sit still if close enough, 70 px band, and it will stand still
Put text on screen for score display = filltext() at position 100, 100
Set, update, and show score value on screen = both scores start off as 0 when ball resets, meaning didnt catch, do Player2Score += 1 or Player2Score++ and Player1Score++
Give ball control based on where it hits on paddle = has to do with angle when bounces off paddle, reflecting horizontal speed, affects vertical speed of ball relation between ballSpeedY and part of paddle. If it hits middle go back to horizontal line, var deltaY = ballY - PADDLE_HEIGHT/2
Reset both scores when either team wins = order matters, score then reset, so you know your calculating most recent score, turn off computer movement for testing
Stop the game when either side wins = add var if true add lock to screen, if showWInScreen return, take you out of loop, nothing will execute
Restart upon mouse click when viewing end screen - connect another event function, when mouse event goes down, if showing win screen, 0 out the scores and turn off show with screen, dont 0 them out at ball resent, because then we can't show score later
Declare on end screen which paddle sided won = don't need or, different messages for who one
Draw dashed line net down playfield center = start var i at 0 go up to 600, jumping 40 px at a time, at each location drawRect(), each location will draw it

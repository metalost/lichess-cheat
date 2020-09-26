# Lichess-Cheat
Simple chess cheat for lichess based on opencv.
#
![Showcase](https://raw.githubusercontent.com/ofeksadlo/lichess-cheat/master/showcase.gif)

# What it does
Creates a new board window which shows you the best next move. For
you and your opponent.

# How it works?
The program captures every 501 milliseconds the board. And then loops through every cell
to detect if a piece moved. If a piece moved it append to the game moveset. Then the program
will feed the stockfish engine with the game movesets in order to get the best next move.

The method is quite easy actually. In order to get prediction for next moves we need to detect which pieces already moved.
In lichess site it's done by drawing the green color around the cell. So we need to detect 2 specific cells.
One green cell without a piece in it (Where the piece moved from) and one green cell with a piece in it (Where the piece moved to).
The detection is done by color matching.
Now we have the last moveset and we can feed are stockfish engine to get predictions.

# Requirements
1) Pyautogui - in order to snap the images https://pypi.org/project/PyAutoGUI/
2) Open-cv - https://pypi.org/project/opencv-python/
3) Stockfish - https://pypi.org/project/stockfish/
4) Numpy - https://pypi.org/project/numpy/
5) Pynput - https://pypi.org/project/pynput/
6) Win32gui - https://pypi.org/project/win32gui/

# How to make it work
1) Download the main.py and the data folder
2) Download stockfish from here: https://stockfishchess.org/download/ I'v used "64-bit: Maximally compatible but slow."
3) You need to extract the exe file you downloaded and in main.py code, change the path to your stockfish engine exe file.
4) About the stockfish.set_depth(16) you can put higher values. The higher the value the more accurate the prediction
   But it's also slower. Using set depth 16 I tied against stockfish level 8 so it's preety strong as it is.
5) Run main.py before the real board is visible. After you run it wait a few seconds so the board window will pop up.
   It's getting prioritized over other windows to stay on top.
   Go to the real board and after 1 move it should start giving you predictions.
6) The program desinged to start at a fresh board. Otherwise it will miss moves that already happend. </br>
   And the predictions will be wrong.
7) In the config.ini you can control which color you start as. And use the auto play function.</br>
   autoPlay On / Off:
   ```sh
   autoPlay=1 / autoPlay=0
   ```
   playerColor White / Black:</br>
   ```sh
   playerColor='w' / playerColor='b'
   ```
   showBoard On / Off:
   ```sh
   showBoard=1 / showBoard=0
   ```
   Default values:
   ```sh
   autoPlay=0
   playerColor='w'
   showBoard=1
   ```
   
   

# Compatibility Issues
The program is far from being perfect. It has a delay because it snap images.</br>
In order to detect pieces and it makes it vulnerable for crashing if the oppenent moved too fast.</br>
The cause is it takes time to detect client move (about half a second). </br>
If the opponent moved faster than that (By preselecting his move). </br>
Then the program will miss the clients move. And any predictions from this point will be wrong.</br>
This can be fixed by detecting last mouse click position. But as far</br>
as education challenge this project is done.</br>
Don't even bother trying Bullet mode. It can barley handle Blitz. In long time modes like Rapid or Classical it works perfectly.
* The program only tested with Chrome on resolution 1920x1080 and the zoom needs to be 100%
* Although the program doesn't snapshot the mouse.</br> Make sure the Board window doesn't get on top of the real board.
* Technically you can make the program to work with any kind of browser on any kind of zoom.
  As long as you fix the cordinates of the board screenshot and the cell size.

# Future plans
* ~~Adding support for black pieces~~ (Added).
* ~~Saving games played~~ (Added).
* ~~Auto Play~~ (Added check it out through the config. Only works for white player)
* Loading game movesets from File.
* Drawing live on the board to highlight best next move.

# Disclaimer 
**This entire project done for the purpose of challenge and education.**<br>
**Not for the purpose of cheating**

**Developed on Python 3.7.7**

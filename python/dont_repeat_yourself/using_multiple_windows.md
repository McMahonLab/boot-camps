[Up To Schedule](../../README.md) - Return To [Write Code for People](../best_practice/Readme.md#step-1-start-at-the-top)

- - - - 

# Working in multiple windows

When anyone starts using a new language like python, it is often convenient to
use an interpreter to explore and experiment.  We are using the iPython
interpreter that allows us to execute python commands and also gives us some
extra capabilities that let us work faster.

However, when the time comes to write a script that you will use over and
over, it is quickly better to work in a separate file that you can run from
the command-line.  At the same time, you may want to test that script while
you are writing it.  It becomes very cumbersome to work in a single window:
* opening the editor
* making changes
* saving the changes
* closing the editor
* running your script
* repeat....

Instead, it is convenient to open multiple windows and arrange them on your
screen so that you can quickly go back and forth between the editor and the
command-line or interpreter where you will run the script.

----

### ![Exercise](../best_practice/pics/exercise.jpg) Short Exercise

1. Open two terminal windows
2. Arrange them on the screen so that one takes the left half and the other
   takes the right half of your screen.
3. In both terminals, navigate to `~/boot-camps/python`
4. Open a text editor (`nano`) in one terminal
5. Open the iPython interpreter in the other terminal
6. In the text editor, type a single line: `print "Hello World!"` and save it as `window1.py`
7. In the iPython interpreter, type `%run window1.py`

**Bonus:** In most operating systems there is a quick way to switch between
  these two windows using the keyboard.  <kbd>Alt</kbd>+<kbd>Tab</kbd> works
  in Windows and linux/unix, while <kbd>Cmd</kbd>+<kbd>Tab</kbd> works on OSX.

----

[Up To Schedule](../../README.md) - Return To [Write Code for People](../best_practice/Readme.md#step-1-start-at-the-top)

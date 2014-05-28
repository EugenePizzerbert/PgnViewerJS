# PgnViewerJS

PgnViewer JS is just a simple JavaScript implementation to show PGN files 
(Portable Game Notation == Chess)
in a web page. There are some tools out there, a lot of them with nice
functionality, but none of them met all my expectations, so this is a try
to meet them all. 

For that purpose, it does not write everything anew, but it uses for that the following libraries:

* [chessboardjs](https://github.com/oakmac/chessboardjs) Chess board that has
 all functionality to display chess positions, move pieces, ...
* [chess.js](https://github.com/jhlywa/chess.js) Base library to model 
  chess in JavaScript

# Features

This implementation will have the following features (in the future):

* Allows to show one or more chess games complete, with a lot of different
  styles, themes, tuning, ...
* Allow to play through the games forward and backward, including variations.
* Allows to play from a legal position only legal moves, and adds these 
  moves to the notation (in a different style)
* Allows to play through
  * clicking on moves
  * clicking on next and previous button
  * clicking on play button
* Knows all PGN notation elements, and knows how to render them.  

# Interface

There are 2 parts to the interface:

   * How does the UI work?
   * How is this viewer used?

## Examples

The included example `examples/sample.html` is my first try how to show 
the board. It will be expanded later by others (complete) examples that 
may be used to study the usage.

To use the examples, you have to first download this repository, and 
open the example files in the browser.
See the different parameters used in this example, to customize the drawing of the board.

The second example `examples/pgn.html` shows the first few moves of a 
game together with the (clickable) notation. This shows (at the moment) 
the deficits I have in using `chess.js` as a library.

The third one `examples/evergreen.html` shows one of the most prominent
games ever, with a beautiful ending. Play through the gmae, and try
to manipulate the CSS and the parameters to see differences.

## Using the viewer

To use the viewer in an HTML page, you have to do the following steps:

   * include the necessary libraries (should be as short as possible)
   * include the necessary CSS files
   * Include a simple JavaScript inside your HTML page.
   * Include the necessary div containers for rendering of the 
   board and the moves

### JavaScript call inside page

    <script>
    cfg = { pieceStyle: 'merida' };
    pgnView("demo",cfg);
    </script>

Alternative call could be:

    <script>
    var pgnData = "1. e4 e5 2. Nf3 Nc6 3. Bb5";
    cfg = { pgn: pgnData };
    pgnView("demo", cfg};
    </script>

There are 3 different options to call the viewer:

1. pgnBoard: The simplest one just to draw a board. This should work
  with a FEN string as argument. If you give a PGN notation, the board
  will render the last position.
2. pgnView: Render a whole game, and allow to play through it. It may
  be (later) possible to add additional boards, and to disable the
  playing funtionality, just to show a static game (e.g. for printing it).
3. pgnEdit: Adds editing functionality, so that the user has the
  option to add (or remove) variants, add comments and PGN notation,
  and to copy at least the current notation to the clipboard, as an
  input for later.
  
### HTML frame

When you use PgnViewerJS, you have to provide a frame for that. The following example is the minimal frame to use.

    <!DOCTYPE html>
    <html>
        <head lang="en">
            <meta charset="UTF-8">
            <title>Simple Example</title>
            <!-- Libraries used: chessboardjs and chess.js from GitHub -->
            <script src="chessboardjs/js/chessboard.js" type="text/javascript"></script>
            <script src="chessboardjs/js/jquery-1.10.1.min.js" type="text/javascript"></script>
            <script src="chessboardjs/js/json3.min.js" type="text/javascript"></script>
            <script src="chess.js/chess.js" type="text/javascript"></script>

            <!-- CSS used: chessboardjs from GitHub -->
            <link href="chessboardjs/css/chessboard.css" type="text/css" rel="stylesheet"/>

        </head>
        <body>
        <div id="board" style="width: 400px"></div>
        <script>Insert here the script</script>

        </body>
    </html>
    
## API
    
Define how the API should look like, and what are the necessary
things users should know to use the viewer in the best way possible.

* Different calls (external API)
  * Arguments to the calls
  * possible attributes of the configuration object
    * in which part is which configuration parameter used
    * are some of them dependent on each other
    * what are the defaults (if there are any)
* Additional calls (internal API)
  * pgnReader: How to read PGN, and what the resulting object
    will have as attributes to be used.
    * Development mode: Creating the parser every time anew (and later how
      to develop the grammar)
    * Runtime mode: Generating and using the parser.
    * Explain the grammar in enough detail.
  * chess: Access to the inner chess game, that allows to move, check, ...
  * board: Access to the inner board, that uses a chess object
  * moves: inner structure of each move, the linking of them, and how to
    find the next and previous moves.
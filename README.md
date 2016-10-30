<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">

<HTML><HEAD><TITLE>Tic Tac Toe</TITLE>
<META http-equiv=Content-Type content="text/html; charset=iso-8859-1">
<META content="MSHTML 6.00.2900.3243" name=GENERATOR></HEAD>
<BODY bgColor=#ffffff>
<CENTER>
<H1>Tic Tac Toe</H1>
<TABLE>
  <TBODY>
  <TR>
    <TD><IMG onclick=squareClick(0); src="Tic Tac Toe_files/blank.gif"></TD>
    <TD><IMG onclick=squareClick(1); src="Tic Tac Toe_files/blank.gif"></TD>
    <TD><IMG onclick=squareClick(2); src="Tic Tac Toe_files/blank.gif"></TD></TR>
  <TR>
    <TD><IMG onclick=squareClick(3); src="Tic Tac Toe_files/blank.gif"></TD>
    <TD><IMG onclick=squareClick(4); src="Tic Tac Toe_files/blank.gif"></TD>
    <TD><IMG onclick=squareClick(5); src="Tic Tac Toe_files/blank.gif"></TD></TR>
  <TR>
    <TD><IMG onclick=squareClick(6); src="Tic Tac Toe_files/blank.gif"></TD>
    <TD><IMG onclick=squareClick(7); src="Tic Tac Toe_files/blank.gif"></TD>
    <TD><IMG onclick=squareClick(8); 
  src="Tic Tac Toe_files/blank.gif"></TD></TR></TBODY></TABLE>
<P>It's currently <IMG src="Tic Tac Toe_files/blank.gif" width=25 
name=whoseTurn>'s turn. 
<P>
<FORM name=tttForm><IMG src="Tic Tac Toe_files/o.gif" width=25> has <INPUT 
size=2 name=xWins> wins.<BR><IMG src="Tic Tac Toe_files/x.gif" width=25> has 
<INPUT size=2 name=oWins> wins.<BR>
<P><INPUT onclick=restartGame(); type=button value="Restart Current Game"> <INPUT onclick=resetCounters(); type=button value="Reset Win Counters"> </FORM>
<P>
</CENTER><SCRIPT language=javascript>

var squares = new Array(9);
var whoseTurn = "x";
var whoWentFirst = "x";
var oWins;
var xWins;

resetCounters();
newGame();

//////////////////////////////////////////////////////////////////////

function resetBoard() {
  var i;
  for (i = 0; i < 9; i++) {
    setSquare(i, "blank");
  }
}

function restartGame() {
  resetBoard();
  if (whoseTurn != whoWentFirst) {
    switchPlayers();
  }
}

function newGame() {
  resetBoard();
  if (whoWentFirst == whoseTurn) {
    switchPlayers();
  }
  whoWentFirst = whoseTurn;
}

function resetCounters() {
  oWins = 0;
  xWins = 0;
  document.tttForm.oWins.value = 0;
  document.tttForm.xWins.value = 0;
}

function squareClick(i) {
  if (squares[i] != "blank") {
    return;  
  } 

  setSquare(i, whoseTurn); 

  if (winBy(whoseTurn)) {
    alert(whoseTurn.toUpperCase() + " wins!");

    if (whoseTurn == "o") {
      oWins++;
    } else {
      xWins++;
    }

    document.tttForm.oWins.value = oWins;
    document.tttForm.xWins.value = xWins;

    newGame();  
  } else if (draw()) {
    alert("Draw!");
    newGame();
  } 

  switchPlayers();
}

function setSquare(i, marker) {
  squares[i] = marker;
  document.images[i].src = marker + ".gif";
}

function switchPlayers() {
  if (whoseTurn == "x") {
    whoseTurn = "o";
  } else {
    whoseTurn = "x";
  }
  document.whoseTurn.src = whoseTurn + ".gif";
}

// board layout:
// 0 1 2
// 3 4 5
// 6 7 8
function winBy(marker) {
  var i;

  // check horizontals
  for (i = 0; i < 7; i = i + 3) {
    if (squares[i] == marker &&
        squares[i + 1] == marker &&
        squares[i + 2] == marker) {
      return true;
    }
  }

  // check verticals
  for (i = 0; i < 3; i = i + 1) {
    if (squares[i] == marker &&
        squares[i + 3] == marker &&
        squares[i + 6] == marker) {
      return true;
    }
  }

  // check diagonals
  if (squares[1] == marker &&
      squares[4] == marker &&
      squares[8] == marker) {
    return true;
  }
  if (squares[2] == marker &&
      squares[4] == marker &&
      squares[6] == marker) {
    return true;
  }

  return false;
}

function draw() {
  var i;
  for (i = 0; i < 9; i++) {
    if (squares[i] == "blank") {
      return false;
    }
  }
  return true;
}

</SCRIPT>
</P></BODY></HTML>

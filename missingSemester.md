# Shell Command Learning:
## Basic Commands
	cd -	cd to the previous location
	>		put the output into a file. for example: echo hi > hello.txt would put "hi" to hello.txt
	<		take something as the input. for example: cat < hello.txt would take the contents from hello.txt and print out
	>>		append instead of replace compared to ">"
	|		wires two commands. example: ls -l / | tail n1 
	curl	
	echo	"value is $foo" -> value is bar; 'value is $foo' -> value is $foo

## Shell Scripting
	$1: first variable;
	$0:name of the script.
	$? error code from previous command
	$_ give last argument from previous command


# Vim

## Modes
### 1.  Insert Mode
  - press "i" to enter
  - press esc to back

### 2. Replace Mode
  - press "R"

### 3. Visual Mode
#### used for selecting words
  - normal visual mode:	press "v"
  - visual line mode:	press "V"
  - visual block mode:	press ^v

### 4. Command Line
  - press ":"

### Normal Mode
	hjkl:	left down up right
	w:		move forward by 1 word.
	b:		move backward by 1 word.
	e:		move to the end of the word
	0:		move to the beginning of the line
	$:		move to the end of the line
	^:		first non-empty character of the line
	^U:		move up one page
	^D:		move down one page
	G:		move all the down
	gg:		move all the way up
	L:		lowest line of the screen
	M:		middle
	H:		highest
	f"x":	find the first appeared "x" after the cursor on the line
	F"x":	find the first appeared "x" before the cursor on the line
	o:		opens a new line below the cursor & put into insert mode
	O:		opens a new line above the cursor & put into insert mode
	dw:		delete a word
	de:		delete to the end of the word
	dd:		delete the entire line
	ce:		delete to the end of the word and enter insert mode
	cc:		delete the entire line and enter insert mode
	x:		delete 1 character
	r"x":	replace the current character with "x"
	u:		undo
	^r:		redo
	y:		copy 1 character
	yw:		copy the word
	yy:		copy the current line
	p:		paste
	%:		jump back and forth between brackets
	di(:	delete the contents within () and enter insert mode
	da(:	delete the contents including () and enter insert mode
	/"xxx":	search for "xxx"
	.:		repeat the previous command
	^N:		autocomplete
	gg=G:	reindent all the lines
	"+y:	copy to system clipboard
	"+P:	paste from system clipboard

## Command-line Environment

### Signals
Check man signal for more info
	
	SIGHUP:		terminate process and hang up.
	SIGINT:		"^C". Terminate process by interrupting the program.
	SIGKILL:	"^\". Terminate process by killing the program (Cannot be caught by program). If there are child processes they will still be on.
	SIGSTOP:	"^Z". Stop process (cannot be caught by program).
	sleep 10 &:	Sleep 10 seconds. The "&" sign means the process would not take over the terminal during the process.
	jobs:		Check current jobs.
	kill %1:	Terminate task 1.
		-STOP:	Suspend the process.
		-HUP:	Hung up the process.
		-KILL:	Kill the process.
	bg %1:		Begin (or continue) processing task 1.
	nohup:		Add a job to the background. Cannot be hunged up (that's why it is called nohup).

### Terminal Multiplexers
  - Sessions
  - Windows
  - Panes


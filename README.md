# Multi-line-cursor-editor
A Python-based multi-line text editor inspired which supports cursor movement, text insertion/deletion, copy-paste, and undo via command inputs.
✏️ Text Editing
Insert text before cursor (i)
Append text after cursor (a)
Delete character (x)
Delete word (dw)
Delete entire line (dd)
📍 Cursor Navigation
Move left/right/up/down (h, l, j, k)
Jump to start/end of line (^, $)
Move by words (w, b)
📄 Line Operations
Insert line above/below (O, o)
Copy line (yy)
Paste above/below (P, p)
🔁 Control Features
Undo previous action (u)
Repeat last command (r)
Command history tracking
👁️ Visualization
Toggle cursor highlight (.)
Toggle row highlight (;)
Display formatted text (s)
🧠 Key Concepts Demonstrated
Data structures (lists for paragraph and memory)
String manipulation
State management (cursor position, history)
Command parsing
Undo/redo logic implementation
Modular programming (functions for each operation)
🏗️ Project Structure
text-editor/
│── main.py
│── README.md
▶️ How to Run
Run the program:
python main.py
Enter commands in the terminal:
> iHello world
> o
> iSecond line
> k
> 0
💡 Example Commands
Command	Description
i<text>	Insert text before cursor
a<text>	Append text after cursor
x	Delete character
dw	Delete word
yy	Copy line
p	Paste below
u	Undo
s	Show content

👩‍💻 Author
Jessica Angela Tyahyo
Data Science Student @ CUHK Shenzhen

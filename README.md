# Multi-line Cursor Editor

A Python-based multi-line text editor inspired by vim. Supports cursor movement, text insertion/deletion, copy-paste, and undo via command inputs.

## ✏️ Text Editing

* Insert text before cursor (`i`)
* Append text after cursor (`a`)
* Delete character (`x`)
* Delete word (`dw`)
* Delete entire line (`dd`)

## 📍 Cursor Navigation

* Move left/right/up/down (`h`, `l`, `j`, `k`)
* Jump to start/end of line (`^`, `$`)
* Move by words (`w`, `b`)

## 📄 Line Operations

* Insert line above/below (`O`, `o`)
* Copy line (`yy`)
* Paste above/below (`P`, `p`)

## 🔁 Control Features

* Undo previous action (`u`)
* Repeat last command (`r`)
* Command history tracking

## 👁️ Visualization

* Toggle cursor highlight (`.`)
* Toggle row highlight (`;`)
* Display formatted text (`s`)

## 🧠 Key Concepts

* Data structures (lists for paragraph and memory)
* String manipulation
* State management (cursor, history)
* Command parsing
* Undo logic
* Modular programming

## 🏗️ Project Structure

```
text-editor/
│── main.py
│── README.md
```

## ▶️ How to Run

```bash
python main.py
```

Example:

```
> iHello world
> o
> iSecond line
```

## 👩‍💻 Author

Jessica Angela Tyahyo
Data Science Student @ CUHK Shenzhen


def help():
    print("? - display this help info")
    print(". - toggle row cursor on and off")
    print("; - toggle line cursor on and off")
    print("h - move cursor left")
    print("j - move cursor up")
    print("k - move cursor down")
    print("l - move cursor right")
    print("^ - move cursor to beginning of the line")
    print("$ - move cursor to end of the line")
    print("w - move cursor to beginning of next word")
    print("b - move cursor to beginning of previous word")
    print("i - insert <text> before cursor")     
    print("a - append <text> after cursor")
    print("x - delete character at cursor")
    print("dw - delete word and trailing spacures at cursor")
    print("yy - copy current line to memory")
    print("p - paste copied line(s) below line cursor")
    print("P - paste copied line(s) above line cursor")
    print("dd - delete line")
    print("o - insert empty line below")
    print("O - insert empty line above")
    print("u - undo previous command")
    print("r - repeat last command")
    print("s - show content")
    print("q - quit program")

def toggle_on(toggle_switch:bool) -> bool:
    """
    Case 1:
    Modifies toggle for cursor.

    Case 2:
    Modifies toggle for row cursor.

    Toggles boolean switch (on <-> off).

    Args:
        toggle_switch (bool): Current toggle state.

    Returns:
        bool: The toggled state.
    """
    return not toggle_switch

def cursor_left(cursor:int) -> int:
    """
    Moves cursor position to left by one character/space
    if not at the beginning.

    Args: 
        cursor (int): index of current cursor position.
    Returns:
        int: updated cursor index.
    """
    return cursor - 1 if cursor > 0 else cursor

  
def cursor_right(cursor:int, cursor_row:int, paragraph:list) -> int:
    """
    Moves cursor position to right by one character/space
    if not at the end.

    Args: 
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        int: updated cursor index.
    """
    if cursor != len(paragraph[cursor_row]) - 1:
        cursor += 1
    return cursor

def cursor_to_beginning():
    """
    Moves cursor position to the beginning of the line.
    
    Args:
        None.
    Returns:
        int: Cursor index 0.
    """
    return 0

def cursor_to_end(cursor:int, cursor_row:int, paragraph:list) -> int:
    """
    Moves cursor position to the end of the line.

    Args: 
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        int: updated cursor index.
    """
    cursor = len(paragraph[cursor_row]) - 1
    return cursor

def cursor_to_next(cursor:int, cursor_row:int, paragraph:list) -> int:
    """
    Moves cursor position to beginning of next word.

    Args: 
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        int: updated cursor index.
    """
    next_space = paragraph[cursor_row].find(" ", cursor)
    if next_space == -1 or next_space == len(paragraph[cursor_row]) - 1:
        return cursor

    cursor = next_space
    while cursor < len(paragraph[cursor_row]) and paragraph[cursor_row][cursor] == " ":
        cursor += 1
    return cursor

def cursor_to_previous(cursor:int, cursor_row:int, paragraph:list) -> int:
    """
    Moves cursor position to beginning of previous word if already
    at beginning of the word the cursor is currently on.

    If cursor is in middle or end of word, move it to the beginning
    of the current word. 

    Args: 
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        int: updated cursor index.
    """
    if cursor == 0:
        return cursor
    if paragraph[cursor_row].find(" ") == -1:
        cursor = 0
        return cursor
    
    current_index = cursor - 1
    while current_index > 0 and paragraph[cursor_row][current_index] == " ":
        current_index -= 1
    while current_index > 0 and paragraph[cursor_row][current_index - 1] != " ":
        current_index -= 1
    cursor = current_index
    return cursor

def insert(cursor:int, cursor_row:int, paragraph:list, text:str) -> list:
    """
    Inserts text to the left of the cursor, the cursor will be at
    the beginning of inserted text.

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
        text (str): text to insert.
    Returns:
        list: updated list of text lines
    """
    if not paragraph: paragraph = [""]
    paragraph[cursor_row] = (
        paragraph[cursor_row][:cursor] + text + paragraph[cursor_row][cursor:]
    )
    return paragraph

def append(cursor:int, cursor_row:int, paragraph:list, text:str) -> tuple[int, list]:
    """
    Appends text to right of the cursor, the cursor will be at
    the end of appended text.

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
        text (str): text to append.
    Returns:
        tuple: updated cursor index and list of text lines. 
    """
    if not paragraph: paragraph = [""]
    if len(paragraph[cursor_row]) == 0:
        cursor -= 1
    paragraph[cursor_row] = (
        paragraph[cursor_row][:cursor + 1] + text + paragraph[cursor_row][cursor + 1:]
    )
    cursor += (len(text))
    return cursor, paragraph
  
def delete_character(cursor:int, cursor_row:int, paragraph:list) -> tuple[int, list]:
    """
    Deletes the character at cursor position.
    Leaves an empty line if all characters at line are deleted.

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated cursor index and list of text lines.
    """
    paragraph[cursor_row] = (
        paragraph[cursor_row][:cursor] + paragraph[cursor_row][cursor + 1:]
    )
    if cursor == len(paragraph[cursor_row]) and cursor != 0: cursor -= 1
    return cursor, paragraph

def delete_while(cursor:int, cursor_row:int, paragraph:list, compare_op:str) -> tuple[int, list]:
    """
    Case1:
    If cursor is on a whitespace, it deletes consecutive spaces forward until it
    is no longer on a whitespace

    Case2:
    If cursor is not on a whitespace, it deletes consecutive spaces forward until it
    is on a whitespace

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
        compare_op(str): comparison operator (either "==" or "!=").
    Returns:
        tuple: updated cursor index and list of text lines.
    """
    while (paragraph[cursor_row][cursor] == " " if compare_op == "=="
           else paragraph[cursor_row][cursor] != " "):
        if cursor == len(paragraph[cursor_row]) - 1:
            return delete_character(cursor, cursor_row, paragraph)
        cursor, paragraph = delete_character(cursor, cursor_row, paragraph)
    return cursor, paragraph

def delete_word(cursor:int, cursor_row:int, paragraph:list) -> tuple[int, list]:
    """
    Deletes all characters from cursor position to beginning of
    next word or to the end of the line.
    Leaves an empty line if all characters at line are deleted.

    If cursor is on a word character, it deletes the word up to the next space
    OR end of the line, then deletes trailing spaces.

    Stops if cursor reaches the end of the line during deletion
    (no next word).

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated cursor index and list of text lines.
    """
    if paragraph[cursor_row][cursor] == " ":
        return delete_while(cursor, cursor_row, paragraph, "==")
    else:
        cursor, paragraph = delete_while(cursor, cursor_row, paragraph, "!=")
    if paragraph[cursor_row] and cursor != len(paragraph[cursor_row]) - 1:
        return delete_while(cursor, cursor_row, paragraph, "==")
    return cursor, paragraph

def line_insert_above(line:str, cursor:int, cursor_row:int, paragraph:list) -> tuple[int, list]:
    """
    Inserts a line above row cursor position, the row cursor follows
    the inserted line position. 

    Args:
        line (string): a string that is inserted above cursor position.
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated cursor index and list of text lines.
    """
    paragraph.insert(cursor_row, line)
    if len(paragraph[cursor_row]) == 0: cursor = 0
    elif len(paragraph[cursor_row]) - 1 < cursor: cursor = len(paragraph[cursor_row]) - 1
    return cursor, paragraph

def line_insert_below(line:str, cursor:int, cursor_row:int, paragraph:list) -> tuple[int, int, list]:
    """
    Inserts a line below row cursor position, the row cursor follows
    the inserted line position. 

    Args:
        line (string): A string that is inserted below cursor position.
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated cursor index, row cursor index, and list of text lines.
    """
    paragraph.insert(cursor_row + 1, line)
    if len(paragraph) != 1:
        cursor, cursor_row = cursor_down(cursor, cursor_row, paragraph)
    return cursor, cursor_row, paragraph

def cursor_up(cursor:int, cursor_row:int, paragraph:list) -> tuple[int, int]:
    """
    Moves row cursor position up by one line. 
    Row cursor stays if already at the top of the paragraph.

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated cursor index and row cursor index.
    """
    if cursor_row != 0 and len(paragraph[cursor_row]) > len(paragraph[cursor_row - 1]):
        cursor = max(0, len(paragraph[cursor_row - 1]) - 1)
    if (cursor_row) != 0: cursor_row -= 1
    return cursor, cursor_row

def cursor_down(cursor:int, cursor_row:int, paragraph:list) -> tuple[int, int]:
    """
    Moves row cursor position down by one line. 
    Row cursor stays if already at the bottom of the paragraph.

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated cursor index and row cursor index.
    """
    if (
        cursor_row != len(paragraph) - 1 and
        len(paragraph[cursor_row]) > len(paragraph[cursor_row + 1])
    ):
        if len(paragraph[cursor_row + 1]) != 0:
            cursor = len(paragraph[cursor_row + 1]) - 1
        else:
            cursor = 0
    if cursor_row != len(paragraph) - 1: cursor_row += 1
    return cursor, cursor_row

def delete_line(cursor:int, cursor_row:int, paragraph:list) -> tuple[int, list]:
    """
    Deletes the whole line (characters, whitespaces, etc) at cursor row.

    Args:
        cursor (int): index of current cursor position.
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
    Returns:
        tuple: updated row cursor index and list of text lines.
    """
    del paragraph[cursor_row]
    if len(paragraph) == cursor_row and cursor_row != 0: cursor_row -= 1
    if not paragraph: cursor = cursor_to_beginning()
    return cursor, cursor_row, paragraph

def copy_line(cursor_row:int, paragraph:list, memory:list) -> list:
    """
    Copies the whole line at cursor row into memory (list).

    Args:
        cursor_row (int): index of current row cursor position.
        paragraph (list): list of text lines (string).
        memory (list): list of lines that have been copied. 
    Returns:
        list: updated list of memory.
    """
    if paragraph: memory.append(paragraph[cursor_row])
    return memory

def show(cursor:int, cursor_row:int, paragraph:list, toggle:bool, toggle_row:bool) -> None:
    """
    Prints the line(s) with OR without cursor highlight OR/AND with or without
    row cursor (* or whitespace).

    Args:
        cursor (int): Index of cursor position within current line.
        cursor_row (int): Index of active row cursor position.
        paragraph (list): List of strings, each string represents a line.
        toggle (bool): Highlights character at cursor position if True.
        toggle_row (bool): Highlights row with prefix "*" if True.

    Returns:
        None.
    """
    for i in range(len(paragraph)):
        prefix = "*" if toggle_row and i == cursor_row else " " if toggle_row else ""
        line = paragraph[i]
        if toggle and (i == cursor_row):
            if len(line) == 1:
                print(prefix + "\033[42m" + line[0] + "\033[0m")
            elif cursor == 0 and len(line) != 0:
                print(prefix + "\033[42m" + line[0] + "\033[0m" + line[1:])
            elif cursor == len(line) and len(line) != 0:
                print(prefix + line[:cursor - 1] + "\033[42m" + line[cursor - 1] + "\033[0m")
            elif len(line) != 0:
                print(prefix + line[:cursor] + "\033[42m" + line[cursor] + "\033[0m" + line[cursor + 1:])
            elif len(line) == 0 and len(paragraph) != 0:
                print(prefix + line)
        else:
            print(prefix + line)

def main() -> None:
    """
    Runs main loop of multi-line text editor.

    Args: 
        None
    Returns:
        None
    """
    # variables
    history = []            # history of all commands except ?, s, u, r, q
    paragraph = []          # editor's content (list of strings)
    memory = []             # list of all copied lines
    text = ""               # inserted or appended text
    cursor = 0              # index position of cursor (initial value is 0)
    cursor_row = 0          # position of row cursor (initial value is 0)
    toggle = False          # when True it highlights element at cursor position
    toggle_row = False      # when True it adds prefix "*" at beginning of line at row cursor position

    while True:
        command = input(">")
        if command == "q":
            break
        if command == "?":
            help()
            continue
        if command == "r" and history:
            command = history[-1][0]
        if command not in ["?", "s", "q", "u", "r"]:
            history.append([command, paragraph[:], cursor, cursor_row])
        if command == "u" and history:
            action = history.pop()
            if action[0] in [".", ";", "h"]:
                if action[0] == ".":
                    toggle = toggle_on(toggle)
                elif action[0] == ";":
                    toggle_row = toggle_on(toggle_row)
                elif action[0] == "h":
                    cursor = cursor_right(cursor, cursor_row, paragraph)
            elif action[0] in ["j", "k", "l"] and paragraph:
                if action[0] == "j":
                    cursor, cursor_row = cursor_down(cursor, cursor_row, paragraph)
                elif action[0] == "k":
                    cursor, cursor_row = cursor_up(cursor, cursor_row, paragraph)
                elif action[0] == "l":
                    cursor = cursor_left(cursor)
            elif action[0] in ["^", "$", "w", "b"] and paragraph:
                cursor = action[2]
            elif action[0][0] in ["i", "a", "x"] or action[0] in ["dw", "dd", "O", "o", "P", "p"]:
                paragraph, cursor, cursor_row = action[1], action[2], action[3]
            elif action[0] == "yy" and memory:
                memory.pop()
        if command in [".", ";", "h", "o", "O"]: 
            if command == ".":
                toggle = toggle_on(toggle)
            elif command == ";":
                toggle_row = toggle_on(toggle_row)
            elif command == "h":
                cursor = cursor_left(cursor)
            elif command == "o":
                cursor, cursor_row, paragraph = line_insert_below("", cursor, cursor_row, paragraph)
            elif command == "O":
                cursor, paragraph = line_insert_above("", cursor, cursor_row, paragraph)
        if command in ["j", "k", "l", "^", "$", "w", "b", "x", "dw", "dd", "yy"] and paragraph:
            if command == "j":
                cursor, cursor_row = cursor_up(cursor, cursor_row, paragraph)
            elif command == "k":
                cursor, cursor_row = cursor_down(cursor, cursor_row, paragraph)
            elif command == "l":
                cursor = cursor_right(cursor, cursor_row, paragraph)
            elif command == "^":
                cursor = cursor_to_beginning()
            elif command == "$":
                cursor = cursor_to_end(cursor, cursor_row, paragraph)
            elif command == "w":
                cursor = cursor_to_next(cursor, cursor_row, paragraph)
            elif command == "b":
                cursor = cursor_to_previous(cursor, cursor_row, paragraph)
            elif command == "x":
                cursor, paragraph = delete_character(cursor, cursor_row, paragraph)
            elif command == "dw" and paragraph[cursor_row]:
                cursor, paragraph = delete_word(cursor, cursor_row, paragraph)
            elif command == "dd":
                cursor, cursor_row, paragraph = delete_line(cursor, cursor_row, paragraph)
            elif command == "yy":
                memory = copy_line(cursor_row, paragraph, memory)
        if command in ["p", "P"] and memory:
            if command == "P":
                cursor, paragraph = line_insert_above(memory[-1], cursor, cursor_row, paragraph)
            else:
                cursor, cursor_row, paragraph = line_insert_below(memory[-1], cursor, cursor_row, paragraph)
        if len(command) > 1 and command[0] in ["i", "a"]:
            text = command[1:]
            if command[0] == "i":
                paragraph = insert(cursor, cursor_row, paragraph, text)
            else:
                cursor, paragraph = append(cursor, cursor_row, paragraph, text)
        if paragraph and (
            command in [
                "s", "u", ".", ";", "h", "o", "O", "j", "k", "l",
                "^", "$", "w", "b", "x", "dw", "dd", "yy", "p", "P"
            ] or (
                len(command) > 1 and command[0] in ["i", "a"]
            )
        ):
            show(cursor, cursor_row, paragraph, toggle, toggle_row)    
main()

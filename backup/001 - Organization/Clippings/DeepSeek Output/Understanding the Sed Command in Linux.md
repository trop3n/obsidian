---
title: "DeepSeek"
source: "https://chat.deepseek.com/a/chat/s/85fde842-6d69-4829-b6cd-dc5dfafee816"
author:
published:
created: 2025-01-17
description: "Chat with DeepSeek AI – your intelligent assistant for coding, content creation, file reading, and more. Upload documents, engage in long-context conversations, and get expert help in AI, natural language processing, and beyond. | 深度求索（DeepSeek）助力编程代码开发、创意写作、文件处理等任务，支持文件上传及长文本对话，随时为您提供高效的AI支持。"
tags:
  - "clippings"
---
The `sed` (stream editor) command in Linux is a powerful tool for processing text in a stream or file. It allows you to perform basic text transformations, such as search and replace, insertion, deletion, and more, without opening the file in an editor. Here's an overview of how `sed` works:

### Basic Syntax

```
sed [options] 'command' input_file
```

- **`options`**: Optional flags that modify the behavior of `sed`.
- **`command`**: The action you want `sed` to perform (e.g., search and replace).
- **`input_file`**: The file to process. If omitted, `sed` reads from standard input.

---

### Common Commands

1. **Substitution (Search and Replace)**:

```
sed 's/old_text/new_text/' input_file
```

- Replaces the first occurrence of `old_text` with `new_text` on each line.
- Add the `g` flag to replace all occurrences globally:

```
sed 's/old_text/new_text/g' input_file
```
2. **Delete Lines**:

- Deletes the `n`th line of the file.
- Example: `sed '3d' input_file` deletes the 3rd line.
3. **Print Specific Lines**:

- Prints the `n`th line of the file.
- Example: `sed -n '5p' input_file` prints the 5th line.
4. **Insert Text**:

- Inserts `text` before the `n`th line.
- Example: `sed '2i\New Line' input_file` inserts "New Line" before the 2nd line.
5. **Append Text**:

- Appends `text` after the `n`th line.
- Example: `sed '2a\New Line' input_file` appends "New Line" after the 2nd line.
6. **Change Lines**:

```
sed 'nc\new_text' input_file
```

- Replaces the entire `n`th line with `new_text`.
- Example: `sed '3c\Replaced Line' input_file` replaces the 3rd line.

---

### Common Options

- **`-n`**: Suppresses automatic printing of lines (useful with `p` command).
- **`-e`**: Allows multiple commands to be executed.

```
sed -e 's/foo/bar/' -e 's/baz/qux/' input_file
```
- **`-i`**: Edits the file in place (modifies the file directly).

```
sed -i 's/old_text/new_text/' input_file
```
- **`-f`**: Reads commands from a file.

```
sed -f script.sed input_file
```

---

### Examples

1. Replace "apple" with "orange" in a file:

```
sed 's/apple/orange/' fruits.txt
```
2. Delete lines 5 to 10:
3. Print lines 20 to 25:

```
sed -n '20,25p' input_file
```
4. Insert a line at the beginning of the file:

```
sed '1i\New First Line' input_file
```
5. Replace "foo" with "bar" globally and save changes to the file:

```
sed -i 's/foo/bar/g' input_file
```

---

### Advanced Usage

- **Regular Expressions**: `sed` supports regex for pattern matching.

```
sed 's/[0-9]\+/NUMBER/g' input_file
```
- **Address Ranges**: Apply commands to specific line ranges.

```
sed '10,20s/foo/bar/' input_file
```
- **Multiple Commands**: Combine commands using `-e` or semicolons.

```
sed -e 's/foo/bar/' -e 's/baz/qux/' input_file
```

`sed` is a versatile tool, and mastering it can greatly enhance your text-processing capabilities in Linux. For more details, consult the `sed` manual (`man sed`).
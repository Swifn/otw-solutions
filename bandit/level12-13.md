# Bandit Level 12 → Level 13

---

## 🎯 Objective

The password for the next level is stored in the file `data.txt`, which is a **hex dump of a file that has been repeatedly compressed**.  
To solve this, you’ll need to reverse the hex dump and unpack the file layer by layer.

---


## 🛠️ Commands Used (with explanations)

- `ls`- Lists files in the current directory.
- `cd` - Change the directory
- `cat` - Outputs the content of a file
- `mktemp` - Creates a unique temp file
  - `-d` - Creates a temp directory
- `cp` - Copies file (into a directory)
- `mv` -  Renames or moves a file
- `gunzip` - Decompresses .gz (Gzip) files
- `bzip2` - Compresses or decompresses .bz2 files
  - `-d` - Tells bzip2 to decompress 
- `tar` - Archive manipulation tool
  - `-x` - Extract files from the archive
  - `-v` - Verbose mode (shows extraction process)
  - `-f` - Specifies the archive file to extract
  - `data.tar` - The tar archive to extract
- `xxd` - Creates a hex dump of a given file or standard input
  - `-r` - Reverses a hex dump back into binary




---

## 🚀 Steps to Solve
1. **Open your terminal**

2. **Run the following command to log into the server**:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

3. **Enter the password**

4. **List the contents of the home directory**:
```bash
ls
```
  - You will see:
    ```bash
    data.txt
    ```


5. **Display the contents of the file `data.txt`**:
```bash
cat data.txt
```
- You should see:
  ```bash
  4␦ 4��hH��D0UP�k�.�"˟�����D�p�QG�l��J��΄�x Fc�����޺�����߰;��␦�4�
  ��px��[�h���oFw9 D���9A���\Ѽ-�1�l�N�(^�@Z@T!��I␦2_=pi@�����(,Q�I��/bݐ'�y��R�E
  ...
  ```

6. **Create a temp directory**:
```bash
mktemp -d
```
  - You should see:
    ```bash
    /tmp/tmp.<tmpname>
    ```

7. **Move `data.txt` into the tmp directory**:
```bash
cp data.txt /tmp/tmp.<tmpname>
```

8. **Move into the tmp directory**:
```bash
cd /tmp/tmp.<tmpname>
```

9. **Convert the hex dump back to binary**:
```bash
xxd -r data.txt data.bin
```

10. **Identify the file type**:
```bash
file data.bin
```
  - you will see:
    ```bash
    data.bin: gzip compressed data, was "data2.bin", last modified: Thu Apr 10 14:22:57 2025, max compression, from Unix, original size modulo 2^32 585
    ```
    
11. **Extract repeatedly**:
    
Repeat the process: identify → rename → decompress.
```bash
mv data.bin data.gz
gunzip data.gz
```
```bash
mv data data.bz2
bzip2 -d data.bz2
```
```bash
mv data data.tar
tar -xvf data.tar
```
  - Eventually, you will see:
    ```bash
    data: ASCII text
    ```

12. **Display the contents of the file `data.txt`**:
```bash
cat data.txt
```

Thats the password for `bandit12`

---

## 🎉 You’ve now completed Level 12 → Level 13!


---

## 🧠 Lessons Learned / Notes
- `xxd -r` is essential for reversing hex dumps.

- The `file` command helps guide your next step - always check before decompressing.

- Handling multiple compression formats requires attention to detail and order.

- Using a `/tmp` workspace keeps your home directory clean and avoids permission issues.

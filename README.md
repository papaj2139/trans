# trans

Literally just prints the trans flag to your terminal, supports multiple sizes and custom dimensions

![trans](https://github.com/papaj2139/trans/blob/main/sc.png)

![image](https://github.com/user-attachments/assets/dca32fb7-3b88-4234-bb25-11b96ee99a85)

---

## installation

1.  **download:**
    ```bash
    git clone https://github.com/papaj2139/trans.git
    ```

2.  **make it Executable:**
    ```bash
    cd trans
    chmod +x trans
    ```

3.  **move to system-wide location (optional):**
    example using `/usr/local/bin`:
    ```bash
    sudo mv trans /usr/local/bin/
    ```
    *(this will allow running `trans` from anywhere)*

4. **or just quickly**
    ```bash
    git clone https://github.com/papaj2139/trans.git
    cd trans
    chmod +x trans
    sudo mv trans /usr/local/bin/
    ```

## Usage

run the script directly (`./trans`) or using the globally accessible command (`trans`) if moved in installation step 3

to see all available options and presets:
```bash
trans --help
```

**basic Usage (predefined Sizes):**

* prints the default ('small') flag:
    ```bash
    trans
    ```
    *(the same as `trans small`)*

* prints predefined larger sizes:
    ```bash
    trans big
    trans huge
    ```
    * `huge`: by default attempts to fill your terminal's width uses a fixed height (34 lines) and will warn you if your terminal window appears too small vertically asking if you want to proceed

**custom Dimensions (using flags):**

you can override the default dimensions for any size using the `--width` and `--height` flag if you use these flags without specifying `small`, `big`, or `huge` the script defaults to `small` proportions

* specify width only:
    ```bash
    #use default 'small' height, but set width to 60
    trans --width=60

    #use default 'big' height, but set width to 80
    trans big --width=80
    ```

* specify height only:
    ```bash
    #use default 'small' width, but set height to 25
    trans --height=25

    #use default 'huge' width (terminal width), but set height to 50
    #note: Specifying --height disables the automatic terminal size check for 'huge'
    trans huge --height=50
    ```

* specify both width and height:
    ```bash
    #use 'small' proportions, 100 characters wide and 30 lines high
    trans --width=100 --height=30

    #use 'big' proportions, 120 characters wide and 40 lines high
    trans big --width=120 --height=40
    ```

* specify drawing character:
    ```bash
    #draw a small flag using '*'
    trans -c "*"
    #draw a big flag with custom dimensions using "#"
    trans big -w 60 -he 20 --char="#"

**important notes on options**

* short options with valeus (e.g. -w 50) require the value to be next to the argument
* long options with values (e.g., --width=50) use an equal sign
* if you provide a size preset (small, big, huge) and width/height options the explicit width/height options will take precedence
* if no size preset is given and only width/height options are used it implicitly uses the 'small' preset as a base if one of the dimensions is missing (e.g. trans -w 50 will use small's height) If both are given those are used directly
* if no arguments are given trans small is executed

**compatibility:**

should work on most modern distro's and in general *nix with bash and standard command-line tools (`tput`, `printf`, `seq`). tested primarily on Debian and Alpine, konsole and gnome-terminal even works on termux on android!

require a terminal emulator that supports:
* UTF-8 character encoding (to display the `█` character correctly)
* ANSI color escape codes (Truecolor `\033[38;2;R;G;Bm` support recommended for accurate colors but should fall back gracefully on terminals supporting at least 16/256 colors if Truecolor isn't available though the colors might look different)

---

## uninstall

if you moved the script to a system-wide location (like `/usr/local/bin`) during installation:

```bash
sudo rm /usr/local/bin/trans
```

if you only cloned it and ran it from the directory, simply delete the cloned folder:

```bash
rm -rf trans
```

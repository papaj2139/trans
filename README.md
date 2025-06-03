# trans

(DEPRECATED, there's a new version made in C)

literally just prints the trans flag to your terminal, supports multiple sizes, custom dimensions, borders, centering, and a configuration file

![trans](https://github.com/papaj2139/trans/blob/main/sc.png)

![image](https://github.com/user-attachments/assets/dca32fb7-3b88-4234-bb25-11b96ee99a85)

![help](https://github.com/user-attachments/assets/a95cdf1c-ab77-4933-a469-57f53fe784a0)


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
    trans tiny
    trans medium
    trans big
    trans huge
    trans banner
    ```
    * tiny, small, medium, big: fixed width and height preset
    * huge, banner: attempt to fill your terminal's width and use a predefined height
    * huge (and other presets if a large custom height is specified) will warn you if your terminal window appears too small vertically and ask if you want to proceed

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
    ```
* centering and borders:
    ```bash
    #center the default small flag
    trans --center
    
    #draw a big flag with a border
    trans big --border
    
    #draw a medium flag, centered, with a custom border character
    trans medium --center --border --border-char "+"
    
    #draw a tiny flag with a custom border character and color (ansi escape code)
    trans tiny --border --border-char='X' --border-color-esc '\033[38;2;255;255;0m'
    ```
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

## config file
you can set your preferred defaults in a configuration file the script will look for it in these locations, in order:
1. $XDG_CONFIG_HOME/transrc (e.g., ~/.config/transrc)
2. ~/.transrc
create this file and add any of the following variables (using bash syntax):

* TRANS_DEFAULT_SIZE="big" (e.g., "tiny", "small", "medium", "big", "huge", "banner")
* TRANS_DEFAULT_CHAR="@" (any single character)
* TRANS_DEFAULT_WIDTH=50 (positive integer)
* TRANS_DEFAULT_HEIGHT=20 (positive integer, min 5)
* TRANS_AUTO_CENTER="true" (or "false")
* TRANS_BORDER_ENABLED="true" (or "false")
* TRANS_BORDER_CHAR="." (any single character)
* TRANS_BORDER_COLOR_ESC="\033[38;2;100;100;100m" (an ANSI escape code string)

precedence of settings:

* command-line arguments (highest precedence)
* configuration file settings
* script's hardcoded defaults (lowest precedence)

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

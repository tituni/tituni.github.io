## Installing Latex for vscode

1. Create a new dev container, select "ubuntu"

2. Install [lualatex](https://linuxvox.com/blog/install-texlive-ubuntu-2404/)

```cmd
    sudo apt update
    sudo apt upgrade
    sudo apt install texlive-full
``` 

3. Run with the PDF viewer

```cmd
    latexmk -pdf -pv -e '$pdf_previewer="start xdg-open %S"' yourfile.tex
```
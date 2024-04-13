## Use XeLatex with VSCode

# Requirements

1. Download MacTeX (5.7Gb):

    [https://tug.org/mactex/mactex-download.html](https://tug.org/mactex/mactex-download.html)

2. Install MacTeX.

3. Add MacTeX installation directory to the path by adding the following line to the .zshrc file:

    ```
    export PATH="/usr/local/texlive/2024/bin/universal-darwin:$PATH"
    ```

4. Open VSCode from a Terminal because when is opened from the Launchpad it uses fish and the PATH is not loaded correctly.

    ```
    user@device ~ % code
    ```

5. Go to 'Extensions' in the 'Activity Bar' and search 'latex'.

6. Install 'LaTeX Workshop' extension.

7. Press 'Shift + command + P' in VSCode to run a command.

8. Run the following command:
    ```
    'Preferences: Open User Settings (JSON)'
    ```

9. Inside the opened file named 'settings.json' update the following entry in the dictionary:
    
    ```
    "latex-workshop.latex.tools": 
        ...
        {
            "name": "xelatexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-xelatex",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        ...
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ],
            "env": {}
        },
        ...
    ```

    To become this:
    
    ```
    "latex-workshop.latex.tools": 
        ...
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-xelatex",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        ...
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ],
            "env": {}
        },
        ...
    ```

10. Add this entry to the dictionary in order to have a recipe that follows the sequence to build correctly with xelatex:

    ```
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex ➞ bibtex ➞ xelatex*2",
            "tools": ["xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        },
        // other recipes...
    ],
    "latex-workshop.latex.recipe.default": "xelatex ➞ bibtex ➞ xelatex*2",
    ```

11. Add this entry to the dictionary to have a visual limit in line length to be used as a reference:
   
    ```
    "editor.rulers": [80,120],
    ```

12. Go to the '.tex' file that you want to build as a pdf.

13. Go to the 'LaTeX' extension in the 'Activity Bar'.

14. Expand the Build LaTeX project option.

15. Select the following option:

    ```
    Recipe: xelatex ➞ bibtex ➞ xelatex*2
    ```

16. If you have some build errors, they can be explained in the 'LaTeX Workshop' and 'LaTeX Compiler' in the Output tab or in the generated .log file with the same name as your built file.
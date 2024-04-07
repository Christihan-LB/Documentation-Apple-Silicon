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

7. Go to the '.tex' file that you want to build as a pdf.

8. Go to the 'LaTeX' extension in the 'Activity Bar'.

9. Expand the Build LaTeX project option.

10. Select the following option:

    ```
    Recipe: latexmk (xelatex)
    ```

11. Maybe you would need to build two times the file in order to generate in the first execution some missing files like: .aux, .bbl, .fdb_latexmk, .fls, .gls.aux, .lof, .lot, .syntex.gz,
# pandoc

Convert markdown to html:

    pandoc input.md -f markdown -t html -s -o output.html

* `-f` specifies which format to convert *from*
* `-t` specifies which format to convert *to*
* `-s` creates a *standalone* document (includes headers and footers)
* `-o` specifies the output file

Fix leading quotation marks and dashes for LaTeX:

    pandoc --smart input.txt -f plain -t latex -o output.tex

* can also use `-S` instead of `--smart`

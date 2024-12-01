# Disk Usage as Postscript

This is a small script I wrote a long time ago to take text output from the `du` Unix command and display it graphically using Postscript.
The bulk of the script is several subroutines written in the Postscript language.
The raw output from du is embedded in the output and is not interpreted until the page is rendered.
There is a small Borne shell script to help collect the du data and generate a few headers and footers.

The output is pure Postscript which may be sent to compatible printers or converted to other formats using Ghostscript or other tools.

## Examples

The stdout is pure Postscript:
```sh
dups /opt/homebrew > summary.ps
```

You may pipe through `ps2pdf14` (provided by Ghostscript) so that a vector pdf file is directly created:
```sh
dups /opt/homebrew | ps2pdf14 - summary.pdf
```
![image](https://github.com/user-attachments/assets/7246c4f8-8665-4e0b-a9b3-97fad2ab436b)

There is an option inside the Postscript file to output a pie chart instead of the default bar chart.
To use this, search for the word *false* and replace it with *true*.
For example, using `sed`:
```sh
dups /opt/homebrew | sed s/false/true/ | ps2pdf14 - summary.pdf
```
![image](https://github.com/user-attachments/assets/d44d99fd-f1a4-4426-a812-593dcdc1d043)

There is no paper size specified in the output.
The chart will automatically use the full paper size it is printed to.
For example, the pie chart will center iteself on any paper size.
```sh
dups /opt/homebrew | sed s/false/true/ | ps2pdf14 -dDEVICEWIDTHPOINTS=2000 -dDEVICEHEIGHTPOINTS=2000 - summary.pdf
```
![image](https://github.com/user-attachments/assets/b7dd6090-ec1d-478f-84c7-dea92c2e93e7)

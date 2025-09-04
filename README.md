# VLBI_calibrated_troposphere_2018_2025 
   

Here are presented the files with already self-calibrated troposphere and clock for VLBI experiment from 2018 to 2025. Troposphere parameters and clock offset
are estimated as stochastic parameters with
priori covariance functions for each
observational epoch. That they added to the constant value of troposphere and clock offset.

Each arcive containts following files:
1) ***.ngs**: typical ngs-file.
2) **trop_clock.dat**: file with troposphere parameters. 
MJD, first_station, second_station, source,  north-south gradient for first_station, north-south gradient for second_station,   east-west gradient for first_station,
 east-west gradient for secind_station, clock offset.

4) ***.txt**: ngs-file  with troposphere calibation. New NGS file contains wet troposphere delay and
gradients and clock offset (ns).
5) **collocat.opt**: This file contains a list of all stations.
6) **baseline.eli**: If exists, contains baselines that needs to be cut out from the observations.
7) **breaks.res**:  If exists, contains  clock breaks on stations.

#  Example of *.txt file structure:
Below is an example of a block from  *.txt file. 

In 504 line there are troposphere for the 1st  ‭(HART15M) and 2nd  ‭( MATERA) station, north-south gradient for stations 1st and 2nd, 
east-west gradient for stations 1st and 2nd, clock offset.

<pre>  HART15M   MATERA    0454-234 2020 03 09 17 00  10.0000000000               501                
   11236439.13979774   0.01029  -258978.2003969568   0.08722 0      I        502                
   0.00174    .00000    .00000    .00000   2.183861602369427       0.0       503  
  0.502   0.249  0.0001  0.0096  0.0009 -0.0009     -17476.438               504
   0.00000   0.10605    .00000    .00000    .00000    .00000                 505                
    21.800     7.704   863.006   953.000    61.389    66.773 0 0             506 </pre>  

All you need now is subtract  troposphere and clock parameters (line 504) and process experiment using the standard least squares method.
 ```fortran  
    IF (ICD1.EQ.4) then
      
        READ (LINE,310) tr1, tr2, trgn1, trgn2, trge1, trge2, delay_c
        

310     format (f7.3,1x,f7.3,4(1x,f7.4),f15.3)

C     DELAY IS IN NANOSECS

         DELAY_t = tr2 - tr1 + trgn2 - trgn1 + trge2 - trge1                    !  delay in nsec

         delay = delay - delay_t  - delay_c    !    nsec     

      end if 
 ```

# How to downoald all files?
 You can download individual experiments by cliking on zip-archive and download row file.

1)  Just click the green **Code** button at the top right, then select **Download ZIP**.

2) Using *git* via terminal / command line.

**Installation on Linux (Ubuntu):**

Open terminal and run:

```bash
sudo apt update
sudo apt install git
git clone https://github.com/Gelochka/VLBI_calibrated_troposphere_2018_2025.git
```
To Unzip all archives: 

```bash
cd VLBI_calibrated_troposphere_2018_2025
find . -type f -name '*.zip' | while read f; do unzip "$f" -d "$(dirname "$f")"; done
```
 **Installation on Windows:**

Install git on Windows: https://github.com/git-for-windows/git/releases/tag/v2.51.0.windows.

After installing Git on Windows, right-click inside any folder and select **"Git Bash Here"**,  
or open **Git Bash** from the Start menu. Then run:

```bash
git clone https://github.com/Gelochka/VLBI_calibrated_troposphere_2018_2025.git
cd VLBI_calibrated_troposphere_2018_2025
find . -type f -name '*.zip' | while read f; do unzip "$f" -d "$(dirname "$f")"; done
```

2) Using *git* via terminal / command line.

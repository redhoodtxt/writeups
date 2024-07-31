*This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify and submit the database password, which is hard-coded in the leaked source code.*

The page gave nothing useful, so i appended `robots.txt` to the URL to find directories hidden:
![[Screenshot 2024-05-08 at 11.25.51 AM.png]]
Accessed the `/backup` to receive the following directory with a file:
![[Screenshot 2024-05-08 at 11.28.20 AM.png]]
Accessed this file to see the database password located in the source code:
![[Screenshot 2024-05-08 at 11.29.06 AM.png]]
Submitted the password to solve the lab.

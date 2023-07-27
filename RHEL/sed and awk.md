`awk -F : '/user { print $4 }' /etc/passwd` -
`awk -F : '/sschlangen {print $4}' /etc/passwd`
![[Pasted image 20220614013906.png]]

`sed -n 5p /etc/passwd`
![[Pasted image 20220614014214.png]] - This print out line 5 out of the `etc/passwd`

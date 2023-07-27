
# SUID

- Set User Identification - When File executed its gets executed as the user id of the owner of the file instead of the user id of the person that is running the file


Useful when using the ``su`` command or the password command

``touch suidfile``

![[Pasted image 20230104183938.png]]


# Set SUID

``chmod 4664 suidfile``

![[Pasted image 20230104184044.png]]


- Notice the " S ". 

``chmod 4764 suidfile``

- "s" = Execute bit and Sticky bit are both set


![[Pasted image 20230104184216.png]]


# Group ID
- works the same way but only applies to the group on a file

``touch sgidfile``
``ls -l``

![[Pasted image 20230104184446.png]]


# Set Group ID
``chmod 2664 sgidfile``

![[Pasted image 20230104184649.png]]

# Set Execute and Sticky Bit in Group ID

``chmod 2674 sgidfile``
``ls -l sgidfile``

![[Pasted image 20230104184822.png]]

# Find Files that have SGID/SUID

``find . -perm /4000``
``find . -perm /2000``

# Set both User and Groups

``touch both``
``chmod 6664 both``

![[Pasted image 20230104185257.png]]


# Stickybit
- Usually set on directories that are shared between people. Allows the user that owns the file to remove that file no matter what permissions are in the directory. Only the user-owner can deleted

``chmod -t stickdir``

``chmod 1777 stickydir``

![[Pasted image 20230104185615.png]]

- notice the " t " - sticky bit and execute bit are set
- ![[Pasted image 20230104185633.png]]

![[Pasted image 20230104185711.png]]


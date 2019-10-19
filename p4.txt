.data

    endl:    .asciiz  "\n"   # used for cout << endl;

    sumlbl:    .asciiz  "Sum: " # label for sum

    revlbl:    .asciiz  "Reversed Number: " # label for rev

    pallbl:    .asciiz  "Is Palindrome: " # label for isPalindrome

    sumarr:    .word 1

               .word 3

               .word 44

               .word 66

               .word 88

               .word 90

               .word 9

               .word 232

               .word 4325

               .word 2321

    arr:       .word 1

               .word 2

               .word 3

               .word 4

               .word 5

               .word 4

               .word 3

               .word 2

               .word 1



.text



# sum               --> $s0

# address of sumarr --> $s1

# rev               --> $s2

# num               --> $s3

# isPalindrome      --> $s4

# address of arr    --> $s5

# i                 --> $t0

# beg               --> $s6

# end               --> $s7

# d                 --> $t1

# 10                --> $t2

# 100               --> $t3

main:

li $t0,0
la $s1,sumarr
li $t2,10
li $s0,0


loop:
beq $t0,10,break
lw $t4,0($s1)
add $s0,$s0,$t4
addi $s1,$s1,4
addi $t0,$t0,1
j loop

break:


li $s3,45689
li $s2,0
li $t1,-1
li $t2,10

loop2:
beq $s3,0,break1
div $t5,$s3,$t2
mul $t5,$t5,$t2
sub $t1,$s3,$t5
mul $s2,$s2,$t2
add $s2,$s2,$t1
div $s3,$s3,$t2
j loop2

break1:

la $s5,arr
li $t0,8
li $t4,4
mul $t0,$t0,$t4
add $t0,$s5,$t0
li $s4,1

loop3:
beq $s5,$t0,break2
lw $t1,0($s5)
lw $t2,0($t0)
bne $t1,$t2,false
addi $s5,$s5,4
addi $t0,$t0,-4
j loop3

false:
li $s4,0
break2:

exit:

  la   $a0, sumlbl    # puts sumlbl into arg0 (a0 register) for cout

  addi $v0, $0, 4     # puts 4 in v0 which denotes we are printing a string

  syscall             # make a syscall to system



  move $a0, $s0       # puts sum into arg0 (a0 register) for cout

  addi $v0, $0, 1     # puts 1 in v0 to denote we are printing an int

  syscall             # make a syscall to system



  la   $a0, endl      # puts the address of the string endl into a0

  addi $v0, $0, 4     # puts 4 into v0 saying we are printing a string

  syscall



  la   $a0, revlbl    # puts revlbl into arg0 (a0 register) for cout

  addi $v0, $0, 4     # puts 4 in v0 which denotes we are printing an string

  syscall             # make a syscall to system



  move $a0, $s2       # puts rev into arg0 (a0 register) for cout

  addi $v0, $0, 1     # puts 1 in v0 to denote we are printing an int

  syscall             # make a syscall to system



  la   $a0, endl      # puts the address of the string endl into a0

  addi $v0, $0, 4     # puts 4 into v0 saying we are printing a string

  syscall



  la   $a0, pallbl    # puts pallbl into arg0 (a0 register) for cout

  addi $v0, $0, 4     # puts 4 in v0 which denotes we are printing a string

  syscall             # make a syscall to system



  move $a0, $s4       # puts isPalindrome into arg0 (a0 register) for cout

  addi $v0, $0, 1     # puts 1 in v0 to denote we are printing an int

  syscall             # make a syscall to system



  la   $a0, endl      # puts the address of the string endl into a0

  addi $v0, $0, 4     # puts 4 into v0 saying we are printing a string

  syscall





  addi $v0,$0, 10

  syscall

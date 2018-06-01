prime_omp.c and prime_pth.c are are parallel programs written in C for determining prime numbers. The
programs works by testing each odd number (up to a specified limit) for divisibility by all of
the factors from 3 to the square root of that number. The algorithm is not very smart, but it is
easy to parallelize.

prime_omp.c use OpenMP and prime_pth.c use Pthreads for parallelism.

# Compile 

Open your terminal and write 
```
$ make
```
That's It.

# Usage
```
Usage: ./primeomp [options]  
-n <num>	Size of input. Maximum number to test  
-p <num>	Number of processors to use  
-o <file>	Output file name  
-d		Display output  
-h 		Display this help and exit  
```
The program takes two main parameters, which are read in from the command line:  
1-P: the number of processors (numProcs in the code); and  
2-N: the problem size (size in the code).  
In addition, the program takes arguments that output all of the primes generated, either to a
file or standard out. Precise usage instructions can be seen by running ./primes –h and
you can make use of the given Makefile.	
		
The main data structure of the program is an array which holds boolean values indicating
whether the corresponding numbers are prime. The array only holds odd numbers, since no
even numbers (except 2) are prime. You should parallelize the actual core code.





# 1. Running Times (Intel core i7-4600u)

## 1.1 Pthread

|      | 200K   | 500K   | 1M     | 2M     | 4M    |
|------|--------|--------|--------|--------|-------|
| 1    | 0,047s | 0,149s | 0,392s | 0,928s | 2,42s |
| 2    | 0,019s | 0,095s | 0,201s | 0,482s | 1,20s |
| 4    | 0,014s | 0,053s | 0,117s | 0,261s | 0,61s |
| 8    | 0,022s | 0,054s | 0,123s | 0,266s | 0,69s |

## 1.2 OpenMP

|      | 200K   | 500K   | 1M     | 2M     | 4M    |
|------|--------|--------|--------|--------|-------|
| 1    | 0,052s | 0,157s | 0,382s | 0,847s | 2,31s |
| 2    | 0,033s | 0,088s | 0,164s | 0,473s | 1,41s |
| 4    | 0,015s | 0,053s | 0,185s | 0,364s | 0,99s |
| 8    | 0,014s | 0,061s | 0,14s  | 0,370s | 0,92s |

# 2.Fastest thread configurations
## 2.1 Pthread

|         | 200K | 500K | 1M   | 2M   | 4M   |
|---------|------|------|------|------|------|
| Thread  | 4    | 4    | 4    | 4    | 4    |
| SpeedUp | 3,35 | 2,81 | 3,35 | 3,55 | 3,96 |

## 2.2 OpenMP

|         | 200K | 500K | 1M   | 2M   | 4M   |
|---------|------|------|------|------|------|
| Thread  | 8    | 4    | 8    | 4    | 8    |
| SpeedUp | 3,71 | 2,96 | 2,72 | 2,32 | 2,51 |

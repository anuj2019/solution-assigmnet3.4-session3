# solution-assigmnet3.4-session3
A. Implement user defined functions within apply function using the 
mtcars data set and produce column wise summary statistics using apply function and mtcars dataset. 
B. write a program to extract the names of the 

list. 


1 What are apply functions?
Apply functions are a family of functions in base R which allow you to repetitively perform an action on multiple chunks of data. An apply function is essentially a loop, but run faster than loops and often require less code.
The apply functions that this chapter will address are apply, lapply, sapply, vapply, tapply, and mapply. There are so many different apply functions because they are meant to operate on different types of data.
2 The apply function
First, let’s go over the basic apply function. You can use the help section to get a description of this function.
?apply
the apply function looks like this: apply(X, MARGIN, FUN).
•	X is an array or matrix (this is the data that you will be performing the function on)
•	Margin specifies whether you want to apply the function across rows (1) or columns (2)
•	FUN is the function you want to use
2.1 apply examples
my.matrx is a matrix with 1-10 in column 1, 11-20 in column 2, and 21-30 in column 3. my.matrx will be used to show some of the basic uses for the apply function.
my.matrx <- matrix(c(1:10, 11:20, 21:30), nrow = 10, ncol = 3)
my.matrx
##       [,1] [,2] [,3]
##  [1,]    1   11   21
##  [2,]    2   12   22
##  [3,]    3   13   23
##  [4,]    4   14   24
##  [5,]    5   15   25
##  [6,]    6   16   26
##  [7,]    7   17   27
##  [8,]    8   18   28
##  [9,]    9   19   29
## [10,]   10   20   30
2.1.1 Example 1: Using apply to find row sums
What if I wanted to summarize the data in matrix m by finding the sum of each row? The arguments are X = m, MARGIN = 1 (for row), and FUN = sum
apply(my.matrx, 1, sum)
##  [1] 33 36 39 42 45 48 51 54 57 60
The apply function returned a vector containing the sums for each row.
2.1.2 Example 2: Creating a function in the arguments
What if I wanted to be able to find how many datapoints (n) are in each column of m? I can use the length function to do this. Because we are using columns, MARGIN = 2.
apply(my.matrx, 2, length)
## [1] 10 10 10
What if instead, I wanted to find n-1 for each column? There isn’t a function in R to do this automatically, so I can create my own function. If the function is simple, you can create it right inside the arguments for apply. In the arguments I created a function that returns length - 1.
apply(my.matrx, 2, function (x) length(x)-1)
## [1] 9 9 9
As you can see, the function correctly returned a vector of n-1 for each column.
2.1.3 Example 3: Using a function defined outside of apply
If you don’t want to write a function inside of the arguments, you can define the function outside of apply, and then use that function in apply later. This may be useful if you want to have the function available to use later. In this example, a function to find standard error was created, then passed into an apply function.
st.err <- function(x){
  sd(x)/sqrt(length(x))
}
apply(my.matrx,2, st.err)
## [1] 0.9574271 0.9574271 0.9574271
2.1.4 Example 4: Transforming data
Now for something a little different. In the previous examples, apply was used to summarize over a row or column. It can also be used to repeat a function on cells within a matrix. In this example, the apply function is used to transform the values in each cell. Pay attention to the MARGIN argument. If you set the MARGIN to 1:2 it will have the function operate on each cell.
my.matrx2 <- apply(my.matrx,1:2, function(x) x+3)
my.matrx2
##       [,1] [,2] [,3]
##  [1,]    4   14   24
##  [2,]    5   15   25
##  [3,]    6   16   26
##  [4,]    7   17   27
##  [5,]    8   18   28
##  [6,]    9   19   29
##  [7,]   10   20   30
##  [8,]   11   21   31
##  [9,]   12   22   32
## [10,]   13   23   33
2.1.5 Example 5: Vectors?
The previous examples showed several ways to use the apply function on a matrix. But what if I wanted to loop through a vector instead? Will the apply function work?
vec <- c(1:10)
vec
##  [1]  1  2  3  4  5  6  7  8  9 10
apply(vec, 1, sum)
If you run this function it will return the error: Error in apply(v, 1, sum) : dim(X) must have a positive length. As you can see, this didn’t work because apply was expecting the data to have at least two dimensions. If your data is a vector you need to use lapply, sapply, or vapply instead



elem<-(c(listdata))
lp<-length(elem)
for (i in 1:lp)
{
    newlist<-c(listdata[[i]][3]) ###maybe to put in a vector
    print(newlist)
 }
When I print the results I get the third element, but like this:
  [1] "1417365_a_at"
  [1] "1416336_s_at"
  [1] "1416044_at"
  [1] "1451201_s_at"
so I cannot traverse them with an index like newlist[3], because it returns NA. Where is my mistake?
r list vector



If you want to extract the third element of each list element you can do:
List <- list(c(1:3), c(4:6), c(7:9))
lapply(List, '[[', 3)  # This returns a list with only the third element
unlist(lapply(List, '[[', 3)) # This returns a vector with the third element
Using your example and taking into account @GSee comment you can do:
yourList <- list(c("","668","12345_s_at","667", "4.899777748","49.53333333",
       "10.10930207", "1.598228663","5.087437057"),
     c("","376", "6789_at",  "375",  "4.899655078","136.3333333",
       "27.82508792", "2.20223398",  "5.087437057"),
     c("", "19265", "12351_s_at", "19264", "4.897730912",
       "889.3666667", "181.5874908","1.846451572","5.087437057" ))

sapply(yourList, '[[', 3)
[1] "12345_s_at" "6789_at"    "12351_s_at"


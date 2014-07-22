ProgrammingAssignment2Rprg
==========================
### Description
The following R functions that are able to create a matrix and get the
value of the inverse and also cache the results and first check if the 
inverse has already been calculated, in order to reduce the time consuming
computation

## Function makeCacheMatrix
makeCacheMatrix creates a matrix, which is really a list containing a 
function to set the value of the matrix, get the value, set the value 
of the inverse and get the value of the mean


<!-- -->

  makeCacheMatrix <- function(x = matrix()) {
    m <- NULL
    set <- function(y) {
      x <<- y
      m <<- NULL
    } 
    get <- function() x
    setsolve <- function(solve) m <<- solve
    getsolve <- function() m
    list(set = set, get = get,
        setsolve = setsolve,
        getsolve = getsolve)
  } 

## Function cacheSolve

The following function calculates the inverse of the matrix created with 
the above function. However, it first checks to see if the inverse has 
already been calculated. If so, it gets the inverse from the cache and 
skips the computation. Otherwise, it calculates the inverse of the data 
and sets the value of the inverse in the cache via the setsolve function.

<!-- -->
  cacheSolve <- function(x, ...) {
          ## Return a matrix that is the inverse of 'x'
    m <- x$getsolve()
    if(!is.null(m)) {
      message("getting cached data")
      return(m)
    }
    data <- x$get()
    m <- solve(data, ...)
    x$setsolve(m)
    m
  } 

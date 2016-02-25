# Continuation-Passing Style
CPS is a particular way of defining and calling functions.

Normal functions take in some arguments, do some computation and return the result.

CPS takes in a callback function as an extra parameter. Instead of returning the result directly, it calls the callback on it.
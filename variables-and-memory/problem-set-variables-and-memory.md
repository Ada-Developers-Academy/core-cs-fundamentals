# Problem Set: Variables and Memory

## Variable Scope
1. The function below has a bug related to variable scope. Fix the bug to pass the tests.
1. The function below has a bug related to variable scope. Fix the bug to pass the tests.
1. What is fahrenheit_temp?


def convert_to_fahrenheit(temp):
    fahrenheit = 2*temp
    return fahrenheight

def convert_to_celsius(temp):
    fahrenheit = 2*temp
    return fahrenheight

celsius_temp = 5
fahrenheit_temp = 32

convert_to_fahrenheit(celsius_temp)
convert_to_fahrenheit(fahrenheit_temp)

print(fahrenheit_temp)

what is fahrenheit?

32


## Variables Are References

1. Immutable Example (string)

a = "hello"
b = a
a = "world"

what is a? what is b?

1. Immutable Example (string)

a = 5
b = a
a += 2

what is a? what is b?

1. Mutable Example (list)

a = [1,2,3]
b = a
a.append(4)

what is a? what is b?

1. Mutable Example (dictionary)
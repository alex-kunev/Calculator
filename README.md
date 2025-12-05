A lightweight C# library that performs basic arithmetic operations and automatically logs usage details to a JSON file.
# Features
 * Arithmetic Operations: Supports Addition, Subtraction, Multiplication, and Division.
 * Automatic Logging: Every operation performed is recorded in a calculatorlog.json file.
 * Error Handling: safely handles division by zero by returning double.NaN.
 * Structured Data: Uses Newtonsoft.Json to produce clean, indented JSON logs.
# Prerequisites & Dependencies
To use this library, your project must have the following installed:
 * .NET SDK (Compatible with standard .NET versions)
 * Newtonsoft.Json (NuGet Package)
You can install the dependency via the .NET CLI:
dotnet add package Newtonsoft.Json

# Usage
1. Initialization
Instantiate the Calculator class. Upon initialization, the library immediately creates (or overwrites) the calculatorlog.json file and prepares the JSON writer.
using CalculatorLibrary;

Calculator calc = new Calculator();

2. Performing Operations
Use the DoOperation method.
Signature:
public double DoOperation(double num1, double num2, string op)

Parameters:
 * num1: The first number.
 * num2: The second number.
 * op: A string representing the operation code.
Operation Codes:
| Code | Operation |
|---|---|
| "a" | Add (num1 + num2) |
| "s" | Subtract (num1 - num2) |
| "m" | Multiply (num1 * num2) |
| "d" | Divide (num1 / num2) |
3. Cleanup
You must call the Finish() method when you are done. This closes the JSON array and flushes the file stream. If this is skipped, the JSON file may be incomplete or invalid.
calc.Finish();

# Example Code
Here is a full example of how to implement the library in a Console Application:
using System;
using CalculatorLibrary;

class Program
{
    static void Main(string[] args)
    {
        // 1. Init
        Calculator calculator = new Calculator();

        // 2. Perform Math
        double sum = calculator.DoOperation(5, 10, "a");      // 15
        double quotient = calculator.DoOperation(10, 2, "d"); // 5

        Console.WriteLine($"Sum: {sum}, Quotient: {quotient}");

        // 3. Close Log
        calculator.Finish();
    }
}

# Logging Output
The library generates a file named calculatorlog.json in the application's working directory.
Example content of calculatorlog.json:
{
  "Operations": [
    {
      "Operand1": 5.0,
      "Operand2": 10.0,
      "Operation": "Add",
      "Result": 15.0
    },
    {
      "Operand1": 10.0,
      "Operand2": 2.0,
      "Operation": "Divide",
      "Result": 5.0
    }
  ]
}

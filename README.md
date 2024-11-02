# Catlog-
Please check the below link for the answer code
import json

# Example JSON data as given
data = {
    "keys": {
        "n": 4,
        "k": 3
    },
    "1": {
        "base": "10",
        "value": "4"
    },
    "2": {
        "base": "2",
        "value": "111"
    },
    "3": {
        "base": "10",
        "value": "12"
    },
    "6": {
        "base": "4",
        "value": "213"
    }
}

# Step 1: Parse and Convert Values to Base 10
points = []
for key, value in data.items():
    if key != "keys":
        x = int(key)  # The x-coordinate is the key of the entry
        base = int(value["base"])
        y = int(value["value"], base)  # Convert the value to base 10
        points.append((x, y))

# Step 2: Implement Lagrange Interpolation to find the polynomial
def lagrange_interpolation(x, points):
    result = 0
    for i, (xi, yi) in enumerate(points):
        term = yi
        for j, (xj, _) in enumerate(points):
            if i != j:
                term *= (x - xj) / (xi - xj)
        result += term
    return result

# Step 3: Calculate f(0) to get the constant term 'c'
constant_term = lagrange_interpolation(0, points)
print("The constant term c is:", constant_term)


-------------------------------------------------------------
import json

# Step 1: Read JSON data from a file
def read_json(filename):
    with open(filename, 'r') as file:
        data = json.load(file)
    return data

# Step 2: Convert the y-values from their given bases to base 10
def decode_values(data):
    points = []
    for key, value in data.items():
        if key != "keys":
            x = int(key)  # Use the dictionary key as the x-coordinate
            base = int(value["base"])
            y = int(value["value"], base)  # Convert the value to base 10
            points.append((x, y))
    return points

# Step 3: Lagrange Interpolation function to find the polynomial at a specific x
def lagrange_interpolation(x, points):
    result = 0
    for i, (xi, yi) in enumerate(points):
        term = yi
        for j, (xj, _) in enumerate(points):
            if i != j:
                term *= (x - xj) / (xi - xj)
        result += term
    return result

# Main function to compute the secret
def find_secret(filename):
    # Load data
    data = read_json(filename)
    
    # Extract keys and determine k value
    n = data["keys"]["n"]
    k = data["keys"]["k"]
    
    # Decode points
    points = decode_values(data)
    
    # Use only the first k points for interpolation (if more than k are given)
    selected_points = points[:k]
    
    # Step 4: Calculate f(0) to get the constant term 'c'
    constant_term = int(round(lagrange_interpolation(0, selected_points)))
    
    print("The secret (constant term c) is:", constant_term)

# Run the function
find_secret("input.json")
-----------------------------------------------
{
    "keys": {
        "n": 10,
        "k": 7
    },
    "1": {
        "base": "6",
        "value": "13444211440455345511"
    },
    "2": {
        "base": "15",
        "value": "aed7015a346d63"
    },
    "3": {
        "base": "15",
        "value": "6aeeb69631c227c"
    },
    "4": {
        "base": "16",
        "value": "e1b5e05623d881f"
    },
    "5": {
        "base": "8",
        "value": "316034514573652620673"
    },
    "6": {
        "base": "3",
        "value": "2122212201122002221120200210011020220200"
    },
    "7": {
        "base": "3",
        "value": "20120221122211000100210021102001201112121"
    },
    "8": {
        "base": "6",
        "value": "20220554335330240002224253"
    },
    "9": {
        "base": "12",
        "value": "45153788322a1255483"
    },
    "10": {
        "base": "7",
        "value": "1101613130313526312514143"
    }
}
Running this code will print the secret (constant term 
𝑐
c) from the polynomial based on the given shares. This solution allows you to solve for the secret using the minimum number of required shares (7 out of 10 in this example).

Let me know if you need any further clarification!

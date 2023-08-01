---
title: "Day 15: Python Libraries for DevOps"
datePublished: Tue Aug 01 2023 13:24:48 GMT+0000 (Coordinated Universal Time)
cuid: clksbzqam000a09la5tlpgn1d
slug: day-15-python-libraries-for-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690896226868/a8f66189-104b-4fab-aa09-4ee73a907145.jpeg
tags: python, opensource, devops, 90daysofdevops, trainwithshubham

---

## What is YAML?

YAML was previously known as "Yet another markup language." But now it is called "YAML ain't markup language."

It is not a programming language. It is basically a data format used to exchange data. It is similar to XML and JSON data types. YAML is a human-readable language that can be used to represent data.

```bash
#YAML Example
person:
  name: John Doe
  age: 30
  gender: Male
  address:
    city: New York
    street: 123 Main Street
  hobbies:
    - Reading
    - Photography
```

## What is JSON?

JSON (JavaScript Object Notation) is a lightweight data interchange format that is easy for humans to read and write and easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language, and it is often used to transmit data between a server and a web application, as an alternative to XML.

```bash
#JSON Example
{
  "name": "John Doe",
  "age": 30,
  "email": "johndoe@example.com",
  "is_active": true,
  "address": {
    "street": "123 Main Street",
    "city": "Anytown",
    "country": "USA"
  },
  "hobbies": ["Reading", "Hiking", "Cooking"]
}
```

## Functions of YAML

* YAML (YAML Ain't Markup Language) is a human-readable data serialization format.
    
* It is often used for configuration files, data exchange between languages, and other structured data representations.
    
* YAML uses indentation and colons to represent hierarchical data structures.
    
* It supports various data types, including strings, numbers, booleans, null, arrays (lists), and objects (mappings).
    
* YAML allows for multiline strings, making it easy to represent long blocks of text.
    
* YAML comments start with the `#` symbol and can be used to provide additional information or explanations.
    

## Functions of JSON

* JSON is a data interchange format used to represent structured data as a string.
    
* In Python, JSON is supported through the `json` module in the standard library.
    
* The `json` module provides functions to work with JSON data in Python.
    
* `json.dumps()`: This function is used to convert a Python object (e.g., dictionary, list) into a JSON-formatted string.
    
* `json.loads()`: This function is used to parse a JSON-formatted string and convert it into a Python object (e.g., dictionary, list).
    
* JSON keys must be strings, and the values can be strings, numbers, booleans, `None`, lists, or other JSON objects (dictionaries).
    

## Task 1: Create a Dictionary in Python and write it to a JSON File.

```python
import json

# Create a dictionary
my_dict = {
    "name": "John Doe",
    "age": 30,
    "is_student": True,
    "hobbies": ["Reading", "Hiking"]
}

# Define the file path for the JSON file
json_file_path = "data.json"

# Write the dictionary to a JSON file
with open(json_file_path, "w") as json_file:
    json.dump(my_dict, json_file, indent=4)

print("Data written to 'data.json'.")
```

After running this code, you will find the JSON data written to a file named `data.json` in the current working directory. The content of the JSON file will be:

```bash
{
    "name": "John Doe",
    "age": 30,
    "is_student": true,
    "hobbies": [
        "Reading",
        "Hiking"
    ]
}
```

## Task 2: Read the JSON file `services.json` kept in this folder and print the service names of every cloud service provider.

```python
import json

# Define the file path for the JSON file
json_file_path = "services.json"

# Read the JSON data from the file
with open(json_file_path, "r") as json_file:
    data = json.load(json_file)

# Extract and print the service names of every cloud service provider
for provider, services in data.items():
    print(f"Cloud Service Provider: {provider}")
    for service in services:
        print(f"- {service['name']}")
    print()  # Add a newline for better readability between providers
```

### **Task 3: Read the YAML file using Python, file services.yaml and read the contents to convert yaml to json.**

```python
import yaml
import json

# Define the file path for the YAML file
yaml_file_path = "services.yaml"

# Read the YAML data from the file
with open(yaml_file_path, "r") as yaml_file:
    data = yaml.safe_load(yaml_file)

# Convert the YAML data to JSON format
json_data = json.dumps(data, indent=4)

# Print the JSON data
print(json_data)
```

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))
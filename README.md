# Check List of Objects for Completeness

A script to check that every object in a list of objects has the same properties. 

# Version 

1.0 Initial

# Global Script Setup
1. Create a Global Script called "CheckObjectListCompleteness"
2. Add the input parameters below to the Global Script
   1. List
3. Add the output parameter below to the Global Script
   1. Complete
4. Drag a *JavaScript* action into the script
5. Add the Javascript below into the JavaScript code property
```javascript
/* Stadium Script v1.0 https://github.com/stadium-software/utils-check-object-properties */
let data = ~.Parameters.Input.List;
let first = JSON.stringify(Object.keys(data[0]).sort());
for (let i=1;i<data.length;i++) {
    if (JSON.stringify(Object.keys(data[i]).sort()) != first) {
        return false;
    }
}
return true;
```
6. Drag a *SetValue* action into the Global Script and place it under the *JavaScript* action
   1. Target: = ~.Parameters.Output.Complete
   2. Value: = ~.Javascript

## Usage
1. Drag the script called "CheckObjectListCompleteness" into a script or event handler
2. Enter values for the script input parameters
   1. List: The List of objects to check
3. Result: The script returns 'true' if all objects have the same properties or 'false' if they don't

Example: Pass
```json
[
    {"Name": "John","Instrument": "Guitar"},
    {"Instrument": "Drums", "Name": "Ringo"},
]
```

Example: Fail
```json
[
    {"Name": "John","Instrument": "Guitar"},
    {"Plays": "Drums", "Name": "Ringo"},
    {"Name": "Ringo"}
]
```

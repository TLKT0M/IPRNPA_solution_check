# IPRNPA Solution Checker

## Overview
This project includes a program called `SolutionChecker` that was developed to check solutions of patient-to-room and nurse-to-patient assignment described in our [preprint](https://arxiv.org/abs/2309.10739)

## How it works
The `SolutionChecker` reads two JSON files: an instance file (`instance_file.json`) and a solution file (`sol_file.json`). These files contain information about rooms, patients, nurses and their assignments and requirements. The checker performs a comprehensive check to validate various aspects such as room capacity, gender distribution, maximum workload, nursing staff skills and many other criteria. Finally, it [outputs](#checked_file) a file with the same name as the instance file +"_checked.json".


## Inputs
1. instance_file: Instance file (`instance_file.json`) from the  [Github Project](https://github.com/TLKT0M/PRA_instance_generator)
2. sol_file: Solutionfile (`sol_file.json`) \
    if math_mode = True: look at  [sol_file.json (math_mode = True)](#math_mode_true) \
    if math_mode = False: look at  [sol_file.json (math_mode = False)](#math_mode_false)
3. weighted_obj_weights = view our [preprint](https://arxiv.org/abs/2309.10739)
4. math_mode = True/False
5. three_shift = True/False \
    False: transfers and violations only in early shift \
    True: violations calculated in every shift

## Inputfiles <a name="Inputfiles"></a>
### sol_file.json (math_mode = True)  <a name="math_mode_true"></a>
```{
    "y": {
        "1": { // patient 1
            "1": { // room 1
                "1": 0, // Shift 1: not assigned (0)
                "2": 1, // Shift 2: assigned (1)
                "ps": 1 // Shift ps: are (all/all early) shifts that the patient needs a bed
            },
            ...,
            "r": { // room r
                "1": 0,
                "2": 0,
                "ps": 1 
            }
        },
        "p": { // patient p
            "1": { // room 1
               ...
            },
            ...,
            "r": { // Room r
                ...
            }
        }
    },
    "x": {
         "1": { // patient 1
            "1": { // Nurse 1
                "1": 0, // Shift 1: not assigned (0)
                "2": 1, // Shift 2: assigned (1)
                "ps": 1 // Shift ps: are all shifts that the patient needs a bed
            },
            ...,
            "n": { // Nurse n
                "1": 0,
                "2": 0,
                "ps": 1 
            }
         },
         "p": { // patient 1
            "1": { // Nurse 1
                ...
            },
            "n": { // Nurse n
                ...
            }
         }
    }
}
```

### sol_file.json (math_mode = False) <a name="math_mode_false"></a>
```
{
    "1": { // shift 1
        "1": { // room 1
            "55": 12, // Patient 55: Nurse 12
            "23": 12, // Patient 23: Nurse 12
        },
        "r": { // room r
            "12": 1, // Patient 12: Nurse 1
        }
    }
    "s": { // shift s
        "1": { // room 1
            "55": 12, // Patient 55: Nurse 12
            "23": 12, // Patient 23: Nurse 12
        },
        "r": { // room r
            "12": 1, // Patient 12: Nurse 1
        }
    }
}
```

## Solution File <a name="checked_file"></a>
The `<instance_name>_checked.json` is placed in the same directory as the instance file. The solution file contains json with the following points
1. "errors": violations of the hard constraints
2. "violations": violations of the soft constraints
3. "transfers": list of transfers 
4. "objectives": list of the objectives and the associated values


## Features
- Calculate objective values
- Check of room capacity and gender distribution.
- Verification of maximum workload and nursing staff skills.
- Calculation of penalties for patient transfers and equipment violations.
- Verification of age distribution and fairness of assignments.
- Conversion of mathematical solutions into a readable format (if required).


For questions about the Solutionchecker, please contact Tom Lorenz Klein (tom.klein[@]tum.de)

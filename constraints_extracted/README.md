# Constraints extracted

The input information and constraints extracted for each API is stored in a `yaml` file.

### The structure of the `yaml` files:

```
link: https://link/to/the/document/webpage
package: <one of tensorflow/torch/mxnet>
target: <API name>
title: <API full name>
version: <version>

inputs
└─── required
│   └─── <required_param1>
│   └─── <required_param2>
│   └─── ...
└─── optional
    └─── <optional_param1>
    └─── <optional_param1>
    └─── ...

constraints
└───<optional_param1>
│   └─── descp: <description of the parameter, parsed from the document>
│   └─── doc_dtype: <dtype of the parameter, parsed from the document>
│   └─── default: <default value of the parameter, parsed from the document>
│   │
│   │  # the following information are all constraints extracted by DocTer
│   │
│   └─── dtype: 
│   │     # Constraint: a list of valid dtype
│   │     └─── <dtype1>
│   │	    └─── <dtype2>
│   │	    └─── ...
│   └─── structure: 
│   │     # Constraint: a list of valid data structure
│   │     └─── <structure1>
│   │	    └─── <structure2>
│   │	    └─── ...
│   └─── tensor_t: 
│   │     # Constraint: a list of valid tensor type (belongs to "structure" category as presented in the paper)		
│   │     └─── <tensor_t1>
│   │	    └─── <tensor_t2>
│   │	    └─── ...
│   └─── shape: 
│   │     # Constraint: a list of valid shape
│   │     └─── <shape1>
│   │	    └─── <shape2>
│   │	    └─── ...
│   └─── ndim: 
│   │     # Constraint: a list of valid ndim (number of dimension)
│   │     #  represented as integers or other variations.
│   │	    #  (belongs to the "shape" category as presented in the paper)
│   │     └─── <ndim1>
│   │	    └─── <ndim2>
│   │	    └─── ...
│   └─── range: 
│   │     # Constraint: a list of valid range (belongs to the "valid value" category as presented in the paper)	
│   │     └─── <range1>
│   │	    └─── <range2>
│   │	    └─── ...
│   └─── enum: 
│        # Constraint: a list of enumerated values (belongs to the "valid value" category as presented in the paper)
│         └─── <enum1>
│ 	      └─── <enum2>
│ 	      └─── ...
└───<optional_param2>
│         ...
└───<required_param1>
│	  ...
└───<required_param2>
	  ...


dependency:
   # the placeholder variables
    └─── <dependency_variable1>
    └─── <dependency_variable2>
    


```



For each parameters, we store the extracted contraints in 7 fields:

- `dtype` : data type of the parameter or the elements of `structure`
- `structure`: data structure of the parameter, e.g., list, tuple.
- `tensor_t`: tensor type (e.g. tensor, sparsetensor)
- `shape`: shape of the parameter
- `ndim`: number of dimension of the parameter
- `range`: valid range of the parameter or the elements of  `structure`
- `enum`: enumerated values  (e.g., "parameter padding can only be one of 'zeros', 'border', and 'reflection'.")



In the paper, to better illustrate the constraints, we further merge some of the fileds to become **four categories**:

- `dtype`
- `structure`: merged from `structure` and `tensor_t`
- `shape`: merged from `shape` and `ndim`
- `valid values`: merged from `range` and `enum`



The `dependency` field stores the depedency variables. For example, `x` from Table1 row1, and `num_classes` in Table1 row2.  


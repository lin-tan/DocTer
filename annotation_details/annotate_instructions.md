### Text that we consider:
- Description
- doc_dtype (only for mxnet and pytorch). It is the string within the parantheses in the document (e.g., https://pytorch.org/docs/stable/generated/torch.nn.Conv1d.html#torch.nn.Conv1d)
- default value 

### "Descp" col:
- Description: the whole description for the parameter
- Doc_dtype: `DD: <doc_dtype text>`
- Default value: `DF: <the default value>`

### Normalization (Col "Normalized_descp"):

#### Normalization for the doc_dtype and description
- `D_TYPE` for data types. 
- `D_STRUCTURE`: for data structures including tensors (e.g., list, tuple, tensor, dict)
- `SHAPE`: strings in brackets which is normally shape, e.g., "shape `[1,1]`" will be normalized to shape `SHAPE`
- `ENUM`: strings in quotation marks (`, ', "). Normally enumerated type or range
- `PARAM`: the parameter's name of the same API. Note that we only normalize the parameter's name with more than one character. For example, we won't normalize the parameter `x` ot `a` to `PARAM` since it only has one character. 
- `CONSTANT_NUM`: contant number (integer)
- `CONSTANT_FLOAT`: constant float
- `CONSTANT_BOOL`: constant boolean (true or false)
- `REXPR`: relational expression, e.g., "a<=1" would be normalized to "a REXPR"

#### Normalization for default value:

There are four cases for the default value's normalization:
- `DEFAULT CONSTANT_NUM`: when the default value is an integer
- `DEFAULT CONSTANT_FLOAT`: when the default value is a float
- `DEFAULT CONSTANT_BOOL`: when the default value is a boolean constant (true/false)
- `DEFAULT DF_STR`: when the default valus is a string. 
- `DEFAULT <the default value >`: for some other cases 

#### `ONE_WORD`
To build the tree structure, we add `ONE_WORD` before the normalized text when there is only one word. 

For example, since the doc_dtype is usually one word, the normalized version of "NDArray" would be `ONE_WORD D_STRUCTURE`.



### Annotation

The are 6 cols to fill and their common values:
- dtype (`D_TYPE`, int, float, bool, string)
- structure: including data structure and tensor type  (e.g., `D_STRUCTURE`, list, dict)
- shape (e.g., `SHAPE`, [2])
- ndim (e.g., `CONSTANT_NUM`, 0, 1)
- range: ( e.g., [0,inf))
- enum (e.g., `ENUM`)


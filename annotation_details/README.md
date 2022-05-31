# Annotation Details



We share the following annotation details:

- `./keywords_tensorflow.yaml`, `./keywords_pytorch.yaml`, `./keywords_mxnet.yaml`:The keywords we used for normalization (Section 2.2). The keywords are collected from the supported data types specified by each library [1][2][3]. We then expand such lists with informal variations. 
- `./assumptions.md`: The assumptions we use during annotation (Section2.2). 
- `./annotation_tensorflow.csv`, `./annotation_pytorch.csv`, `./annotation_mxnet.csv`: the annotations for the 30% parameters. 
- `./annotate_instructinos.md`: the annotation instruction for the annotator.


**References**

[1] 2020. tf.dtypes.DType. https://www.tensorflow.org/versions/r2.1/api_docs/python/tf/dtypes/DType

[2] 2019. torch.Tensor. https://pytorch.org/docs/1.5.0/tensors.html

[3] 2019. incubator-mxnet. https://github.com/apache/incubator-mxnet/blob/1.6.0/python/mxnet/ndarray/ndarray.py#L64-L74



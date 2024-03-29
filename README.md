# UNETR-train
In this jupyter notebook, the UNETR architecture is implemented and trained on Breast Cell dataset for 2D segmentation.

## Dataset
Breast Cell Segmentation dataset is used for training and evaluating this model which consists of images and masks of benign and malignant breast cells in .TIF format.

## Architecture
The architecture begins by accepting image inputs, dividing them into a set of patches, the shape defined as (none, number of patches, patch size * patch_size * number of image channels). Following this, the patch embeddings are created. The patches stick to a set sequence which is described to the model as position embeddings. These patches go through the transformer encoder which begins with a normalization layer, multi-head attention block, residual connection from the embedded patches. The added result is passed through another normalization layer to the multi-layer perceptron with GeLu activation followed by another residual connection. The transformer encoder is repeated according to the number of layers, which is 12 in our case. The CNN decoder starts by reshaping the patches from every skip connection to (height, width, number of filters). The first decoder, 'Decoder 1,' employs deconvolution operations and concatenation with skip connections to upsample and refine the features. Subsequent decoders ('Decoder 2' to 'Decoder 4') follow a similar pattern, gradually increasing the spatial resolution while incorporating information from the skip connections. The output layer is defined at the end with a sigmoid function for binary segmentation.

## Hyperparameters
The model is compiled using binary_crossentropy as loss with adam optimizer and a learning rate of 0.0001. The IoU score is used as the evaluation metric. The batch size and epochs are kept low due to lack of computational power.

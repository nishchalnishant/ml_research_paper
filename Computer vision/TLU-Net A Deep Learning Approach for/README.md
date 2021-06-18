TLU-Net: A Deep Learning Approach for Automatic Steel Surface Defect Detection

>> Abstract -

- steel surface defect is predominantly detected using manual visual inspection as there are many inacuracies with the automatic visual inspection (AVI) method .

- In this paper researchers are using transfer learning based u net framework for faster and more accurate defect detection 

- Researchers have proposed the U net artitecture as the base and explored 2 kinds of encoders ResNet and DenseNet using random initialization and trained on the ImageNet dataset 

- Experiments are performed using Severstal data.

- Final results demonstrate that transfer learning performs 5% better than random initialization in defect classification while 26% better than defect segmentation .

- In addition to above gains the need for data for training is reduced as well as convergance rate has improved .

>> Introduction -

- Manual detection can be replaced or aided by the automatic defect detection leading to better and consistent quality control .

- Defect detection can be divided into 2 main steps 
    * classify the defect type from the image
    * identify the location of the image 

- Although there are various methods for defect localization such as one step and two step localization but each comes with their own disadvantages , thus researchers have proposed the transfer learning based u net .

>> PROPOSED TRANSFER LEARNING BASED U-NET

- The architecture takes an input image of dimension H × W and classifies each pixel to be one or more type of the defect. It involves mainly four parts 
    * The U-Net architecture
    * The type of initialization
    * Classification 
    * objective function

    The u-net architecture
        - encoder decoder artitecture
        - encoder encodes the image using an encoder block and reduces the resolution using pooling while decoder upsamples the representation in every step.
        - skip connection can enable the decoder to select the feature at a different scale to make a more accurate prediction of the object boundaries.

    The type of initialization
        - used 2 kinds of encoder blocks for transfer learning ,both trained on image net dataset 
        - ResNet 
            -deep cnn network with skip connections after each block to handle vanashing gradient problem.
            - we used batch normalization for each block with relu activation function 

        - DenseNet -
            - Dense CNN networks where feature map of the lth layer is connected with the feature map of previous layer 
            it has more number of parameters than ResNet 

    Classification -- 
        - we used spatial average pooling the encoder output to extract the image representation .
        - That image representation us passed through linear activation function with sigmoid activation to enable multi label classification 

    Objective function --
        -  joint segmentation and classification problem is formulated as a weighted combination of the two losses.

            here ,
            BCE -- binary cross entropy loss
            k -- data point index
            m defect class index
            i,j -- spatial index
            y_hat -- predicted probability
            y - ground truth defect label 

>> EXPERIMENTS AND RESULTS

- Data set and preprocessing --
    - data is from kaggle competition "Severstal: Steel Defect Detection".
    - The training set includes 12568 images, and 6666 of them
      include at least one defective region. 
    - Resolution of images is 256x1600 px.
    - We normalize the image using the global mean and standard deviation. 
    - We apply a random vertical/horizontal flip as data augmentation. 
    - The same augmentation applies to both the original image and the corresponding ground truth masks to pair with the augmented images.

- Experimental Setup --
    - 75% data for the training
    - 12.5 % data for validation
    - 12.5% data for the testing.
    - Batch size -16
    - we used adam optimizer with learning rate of 5 × 10−4, β1=0.99 and β2=0.99
    - Trianed the model for 10 epochs with early stopping 
    - implemented in pytorch with pytorch image segmentation library 
    - To understand the model’s sample complexity, we also train these networks using 50% of the training data. We refer to the pretrained initialization as TLU-Net and the random initialization as just U-net.

- Evaluation metrics --
    - We evaluate the steel defect classification performance using multi-label classification accuracy (MLA) and the average area under receiver operating curve (AUC) across 4 classes . 


  

# DECIMER-Image-to-SMILES
The repository contains the network and the related scripts for auto-encoder based Chemical Image Recognition 

### The project contains code which weas written throughout the project (Continuously updated)

#### Top-level directory layout
```bash

  ├── Network/                           # Main model and evaluator scripts
  +   ├ ─ Trainer_Image2Smiles.py     # Main training script - further could be modified for training
  +   ├ ─ I2S_Data.py                 # Data reader module for training
  +   ├ ─ I2S_Model.py                # Autoencoder network
  +   ├ ─ Evaluate.py                 # To Load trained model and evaluate an image (Predicts SMILES)
  +   └ ─ I2S_evalData.py             # To load the tokenizer and the images for evaluation
  +    
  ├── Utils/                              # Utilities used to generate the text data
  +   ├ ─ Deepsmiles_Encoder.py        # Used for encoding SMILES to DeepSMILES
  +   ├ ─ Deepsmiles_Decoder.py        # Used for decoding DeepSMILES to SMILES
  +   ├ ─ Smilesto_selfies.py          # Used for encoding SMILES to SELFIES
  +   ├ ─ Smilesto_selfies.py          # Used for encoding SELFIES to SMILES
  +   └ ─ Tanimoto_Calculator_Rdkit.py  # Calculates Tanimoto similarity on Original VS Predicted SMILES
  + 
  ├── LICENSE
  ├── Python_Requirements                 # Python requirements needed to run the scripts without error
  └── README.md
  
  ```

## Installation of required dependencies:

### Installation of TensorFlow
- This can be done using pip, check the [Tensorflow](https://www.tensorflow.org/install) website for the installation guide. DECIMER can run on both CPU and GPU platforms. Installing Tensorflow-GPU should be done according to this [guide](https://www.tensorflow.org/install/gpu).

### Requirements
  - matplotlib
  - sklearn
  - pillow
  - deepsmiles

## How to set up the directories:

- Directories can be easily specified inside the scripts.
  - The path to the SMILES data is specified in: I2S_Data.py 
  - The path to the Image data is specified in: Trainer_Image2Smiles.py
  - The path to checkpoints will be generated in the same folder where your Trainer script is located, If you would like to use a different path it can be modified in Trainer_Image2Smiles.py.
  
 #### Recommonded layout of the directory
 ```bash
  ├── Image2SMILES/
  +   ├ ─ checkpoints/
  +   ├ ─ Trainer_Image2Smiles.py    
  +   ├ ─ I2S_Data.py                 
  +   ├ ─ I2S_Model.py                
  +   ├ ─ Evaluate.py                 
  +   └ ─ I2S_evalData.py            
  + 
  ├── Data/
  +   ├ ─ Train_Images/
  +   └ ─ DeepSMILES.txt
  +
  └── Predictions/
      └ ─ Utils/
       
 ```
## How to generate the data and train Image2SMILES:

- Generating image data:
  - You can generate your images using SDF or SMILES. The [DECIMER](https://github.com/Kohulan/DECIMER/tree/master/src/org/openscience/decimer) Java repository contains the scripts used to generate images that were used for training in our case. You simply have to clone the repository, get the [CDK](https://cdk.github.io) libraries and use them as referenced libraries to compile the scripts you want to use.
  ```bash
  e.g: 
  javac -cp cdk-2.3.jar:. SmilesDepictor.java   # Compiling the script on your local directory.
  java -cp cdk-2.3.jar:. SmilesDepictor         # Run the compiled script.
  ```
  - The generated images should be placed under /Image2SMILES/Data/Train_Images/
 
 - Generating Text Data:
    - You should use the corresponding SDF or SMILES file to generate the text data. Here, the text data is [DeepSMILES](https://github.com/baoilleach/deepsmiles) strings. The DeepSMILES can be generated using [Deepsmiles_Encoder.py] under Utils. Split the DeepSMILES strings appropriately after generating them.
    - Place the DeepSMILES data under /Image2SMILES/Data/
 
 ### Training Image2SMILES
 - After specifying the "paths" to the data correctly. you can train the Image2SMILES network on a GPU enabled machine(CPU platform can be much slower for big number of Images).
 ```bash
 $ python3 Image2SMILES.py &> log.txt &
 ```
 - AFter the training is finished, you can use your images to test the model trained using the Evaluate.py. in order to generate a completely new set of test data, you can use the same steps as above mentioned to generate training data.

### Predicting using the trained model
- In order to use the trained model provided in the repository please follow these steps;
  - Clone the repository
    ```
    git clone https://github.com/Kohulan/DECIMER-Image-to-SMILES.git
    ```
  - Change directory to Network folder
    ```
    cd DECIMER-Image-to-SMILES/Network
    ```
  - Copy a sample image to the Network folder, check the path to the model inside Predictor.py and run
    ```
    python3 Predictor.py --input sample.png
    ```
## License:
- This project is licensed under the MIT License - see the [LICENSE](https://github.com/Kohulan/Decimer-Python/blob/master/LICENSE) file for details

## Citation
- Use this bibtex tp cite our paper published in Chemrxiv (-todo : update the bibtex of peer reviewed paper)
```
@article{Rajan2020,
author = "Kohulan Rajan and Achim Zielesny and Christoph Steinbeck",
title = "{DECIMER - Towards Deep Learning for Chemical Image Recognition}",
year = "2020",
month = "6",
url = "https://chemrxiv.org/articles/DECIMER_-_Towards_Deep_Learning_for_Chemical_Image_Recognition/12464420",
doi = "10.26434/chemrxiv.12464420.v1"
}
```

## Author:
- [Kohulan](github.com/Kohulan)

![GitHub Logo](/assets/DECIMER_logo.png)

## Project Website
- [DECIMER](https://kohulan.github.io/Decimer-Official-Site/)

## Research Group
- [Website](https://cheminf.uni-jena.de)

![GitHub Logo](/assets/CheminfGit.png)

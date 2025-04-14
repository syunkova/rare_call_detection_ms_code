# Methods for automated detection of rare frog vocalizations
This repository contains supplemental Jupyter notebooks that demonstrate the methods described in a manuscript discussing _Atelopus varius_ call detection, submitted to _Ecological Informatics_ and awaiting review.

## Repository structure
This repository contains 2 environment files, 6 Notebooks, and 4 subdirectories containing sample data.

#### Data folders
- **sample_audio**
    - Contains three 1-minute audio files extracted from real field data used in our study. These files have been examined and confirmed to contain *A. varius* vocalizations.
- **sample_embeddings**
    - Contains three .csv files containing feature embeddings generated using [BirdNET](https://birdnet.cornell.edu/) (Kahl et al., 2023) from the three audio files within **sample_audio**.
- **sample_templates**
    - Contains six 3-second audio segments extracted from training data used in this study. All six files contain _A. varius_ vocalizations.
    - Contains six 1-row .csv files containing feature embeddings generated with BirdNET from the six audio files in the same subdirectory.
- **sample_scores**
    - "Output" directory containing subdirectories to save scores for each method, if desired.

#### Environment files
To run all Notebooks, the user will need to install 2 Python virtual environments using a package manager like [Anaconda](https://anaconda.org/). We provide .yml files to create these environments with required packages:
1. **OpSo011.yml**
    - environment used to run most Notebooks that utilizes [OpenSoundscape](https://opensoundscape.org/en/latest/) version 0.11.0 (Lapp et al., 2023)
2. **OpSo011_tf.yml**
    - environment that integrates OpenSoundscape and two other new packages:
        - [TensorFlow](https://www.tensorflow.org/): needed to run **embed_files.ipynb**, which imports BirdNET, a Tensorflow-based model.
        - [FAISS](https://ai.meta.com/tools/faiss/) (Douze et al., 2024): used to perform efficient embedding similarity search on our embeddings in **embedding_search_demo.ipynb**.
    - These notebooks will not work with the other environment.

#### Notebooks (in suggested order of application)
All Notebooks in this repository are structured similarly: they contain a "setup" section with imports and parameter definitions, a middle "process" section that includes data selection, function definitions, and an actual run-through of the procedure on the attached dummy data, and a final "review" section for the user to preview high-scoring clips, like a tiny portion of the review process described in our study.
1. **cross_correlation_demo.ipynb**
    - Applies template matching by cross-correlation, the first signal processing method described in our study and a "basic" detection method in bioacoustics.
2. **ribbit_demo.ipynb**
    - Applies RIBBIT (Lapp et al., 2021), the only true zero-shot detection method in our study, to the sample test data.
3. **cnn_demo.ipynb**
    - Train and apply a single-class ResNet34 CNN with OpenSoundscape.
4. **embed_files.ipynb**
    - Load BirdNET and use it to embed our data. While this notebook isn't strictly a method used in our study, it serves to generate feature embeddings on our data so that we don't have to rerun that process in following notebooks.
    - Note that, while the order is not critical for all other code in the repository, this Notebook should be run ***before*** **mlp_demo.ipynb** and **embedding_search_demo.ipynb**.
    - Also note that this Notebook must be run with an environment that has TensorFlow (such as *OpSo011_tf*, described above)
5. **embedding_search_demo.ipynb**
    - Query embeddings of our test data for similarities to embeddings of our training data, using FAISS.
5. **mlp_demo.ipynb**
    - Train and apply a shallow neural network - in particular, a Multilayer Perceptron, - using our data.

## Note on Method Performance
The outcome of these scripts may not be the same as described in our manuscript. This discrepancy is due to the amount and sort of data used: because all test data used for these demonstrations was hand-picked from confirmed positive recordings, so the chance of any method successfully detecting the correct sound is much higher - this is in part because all of these method had previously been used in bioacoustics for all sorts of animal sounds. On the other hand, the associated manuscript describes a real-world scenario, where the target vocalization occurs in a very small portion of a very large amount of data (almost 40k 3-minute-long audio recordings) and detection methods need to show very high performance to be successful.

## Manuscript Abstract
> To fill in during review.

## Acknowledgements
I would like to thank Santiago Ruiz-Guzman and Sam Lapp for support in the development and my understanding of methods in this repository, and Justin Kitzes for support and resources in this project.

## Correspondence
Any questions regarding the contents of this repository can be sent to Sasha (Alexandra) Syunkova at > sasha.syunkova@pitt.edu.
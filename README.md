# Photo Culling
Simple project for photo culling. Photo quality scoring is done by a fine-tuned largish image model (VGG-16). Image grouping is done 
by requiring images to have been taken within time_threshold minutes of each other (using their metadata), and having (base) VGG-16 think they're
sufficiently similar (ie cosine similarity of their VGG-16 features greater than similarity_threshold)

**Warning:** The photo quality model still has some unconventional "opinions" about which photos are higher or lower quality, use its advice at your own risk.

### Setup
To set up environment, FIRST install PyTorch, with any required cuda software. Either follow the instructions at 
https://pytorch.org/get-started/locally/ or you can try running the script setup_pytorch.sh in bash or powershell.
Next, install other requirements using pip

``
pip install -r requirements.txt
``

### Running

``
python -m main --image_path samples
``

This will find all images (.jpg, .jpeg, .png) in the "samples" directory, and save 3 files to the directory
'predictions'
- scores.csv - containing two columns: the image path and the scores for each image 
- kept_images.txt, culled_images.txt - containing the filenames of suggested images to be kept vs. culled, one on each line

Alternatively, just the scores.csv file can be produced by adding the --scores_only flag

**Note:** This should *not* delete or move any actual image files

### Credits:
Approach to training by Talebi and Milanfar in https://arxiv.org/pdf/1709.05424v2.pdf.
PyTorch implementation of paper used to train the model by Yunxiao Shi https://github.com/yunxiaoshi/Neural-IMage-Assessment.
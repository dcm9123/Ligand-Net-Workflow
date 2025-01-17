# Ligand-Net-Workflow
This workflow helps the user to determine whether a set of ligands act as actives or decoys when it comes to bind to a specific protein.

## Getting Started
These set of instructions will help you understand and develop a Machine Learning (ML) model to predict ligands as actives or decoys. This workflow generates classification models based on different approach that the user may choose. Those include the following:

* Support Vector Machine (SVM)
* Random Forest (RF)
* Extra Tree Classifier (ETC)
* Neural Networks (NN)

You can either choose one approach to develop a classification model or you may choose all of them. Either way we will run different parameters to find the best model that fits your data; in other words, we will select the one that gives the highest Positive Predictive Value (PPV), sensitivity, and specificity.

## Prerequisites
We need you to have the following in your local computer:
* Anaconda
* Python 3.5 or above
* rdkit 
* tqdm
* sklearn
* mayachemtools
* A folder looking like this:

<img src="https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/folder.png" height="240">

The actives folder should contain at least one `.txt` or `.sdf` file. The decoys folder should contain at least one `.txt` or `.sdf` file as well. Each protein **MUST** have a decoys and an actives file **WITH THE _SAME_ NAME** but found in different folders, for example: /Users/Daniel/Desktop/ligand_net/actives/thromboxane_a2_receptor.txt **AND** /Users/Daniel/Desktop/ligand_net/decoys/thromboxane_a2_receptor.txt
If the files for the decoys and actives do not have the same name, the program will not be able to generate a machine learning model.

Please create a folder called 'actives' and another folder called 'decoys' inside the fingerprints folder. After you do it, you should have something like this:

<img src="https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/inside_fingerprints.png" height="200">

In case you don't have a file for the active ligands, we recommend you running the `looking_actives.py` code found in this repository. Said code needs an accession number (which you can find in the [Pharos website](https://pharos.nih.gov/idg/targets)) of the desired protein. To see how to run this code, please refer to our **Fetching Ligands and Decoys** section.

If you don't have a file for decoys (either in `.txt` or `.sdf`), you may download them through the [DUD-E website decoy generator](http://dude.docking.org/generate) or by using the [DecoyFinder software](http://urvnutrigenomica-ctns.github.io/DecoyFinder/#Downloads_). The latter uses the ZINC database to find a specific number of decoys set by the user; to see how to use it, please refer to our **Fetching Ligands and Decoys** section.

If you don't know how to install any of these packages/modules, please refer to the **Installation** section (below).

## Installation
First, we need to create a Conda python environment. For this, follow the next steps:
1. Install Anaconda 3 from [here](https://www.anaconda.com/download/#linux)
2. Create a new python environment in your terminal:
`conda create -n <env_name> python=3.5 anaconda
source activate <env_name>` (where <env_name> is whatever name you want to give your environment).

For the installation of the remaining packages/modules, keep working in your terminal with the activated environment. 
Then do:
1. `conda install -c rdkit rdkit` 
2. `conda install -c conda-forge tqdm` 
3. `conda install -c anaconda scikit-learn` 
4. Install [mayachemtools](http://www.mayachemtools.org/Download.html) and copy the directory in the folder you created with the other directories shown on the previous image. Once untared and unzipped, you should be able to move to that directory

(i.e.`cd /Users/Daniel/Desktop/ligandnet/mayachemtools/`). 

Inside said folder you should have something like this:

<img src="https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/maya.png" height="240">

## Fetching Ligands and Decoys
If you don't have any ligands you may visit the [Pharos website](https://pharos.nih.gov/idg/targets) and type for a specific protein. After that, you must extract the accession number for it. For instance, if you are looking for the active ligands that bind to thromboxane A2 receptor, the accession number  would be P21731, as it is shown on the image below:

<img src="https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/pharos_website.png" height="300">

Once you have the accession number, you should run the `looking_actives.py` script on your terminal. To run it, type the following: `python looking_actives.py -i <accession_number>`. Following the thromboxane A2 receptor example, the user should type `python looking_actives.py -i P21731`. After that, the terminal should look like this:

<img src="https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/actives_found.png" height="115">

As shown on the image, the code has found 295 ligands for that specific protein, and a `.sdf` file was generated with the accession number as its name. 

If you have the file with the active ligands but not with the decoys, then you may generate those by using the [DUD-E website](http://dude.docking.org/generate) or the DecoyFinder software. If you choose the first, make sure that the ligands are shown in SMILES at the beginning of each line (as shown on the website). If you decide to use the DecoyFinder software, follow the instructions on the website and open the GUI by typing `python decoy_finder.py` in your terminal. Once opened, select the actives file **in `.sdf` format** as input. Where it says "Select local files...", change it to "ZINC all", and click the "add" button. Now, select the options button and select the option "Molecular descriptor based decoys". Go back to the "Find" button, and finally type the path where you want the output file. We recommend to put it where you want your decoys to be tested in this workflow. **Remember to give the same name to your decoys files as it is in your active file**. You should have something like this:

<img src="https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/DecoyFinder_GUI.png" height="400">
## Running the tests

## Contributing
If you wish to contribute, submit pull requests, or read more about our code of conduct, please read [contributing.md](https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/contributing.md)
## Authors
Daniel Castaneda Mogollon, Dewan Shrestha, Md Mahmudulla Hassan, Suman Sirimulla.

See also the list of [contributors](https://github.com/dcastaneda5/Ligand-Net-Workflow/blob/master/contributions) who made this project possible.

## Acknowledgments
We would like to thank everyone at the Sirimulla Research Lab for their effort and support throughout the project. We thank Denise Cano and Govinda KC for generating decoys and running the active/decoys fingerprints. We would also like to thank Dishja Ganjegunte for generating decoys throughout the project.

# AI Video Assistant Referee - Let's Save VAR!

This repository is forked from https://github.com/SoccerNet/VARS. 

If you're looking for technical implementation details and academic background, I invite you to explore the paper published by Jan Held et al. [VARS: Video Assistant Referee System for Automated Soccer Decision Making from Multiple Views](https://arxiv.org/abs/2304.04617).

This repository contains:
 * the SoccerNet-MVFouls, a new multi-view video dataset containing video clips of fouls captured by multiple cameras, annotated with 10 properties.
 * the code for the VARS, a new multi-camera video recognition system for classifying the type of fouls and their severity.
 * my updated version of the VARS interface, which shows the ground truth of the action and the top 2 predictions for the foul classification task, and the offence and severity classification task with the corresponding confidence scores.

Note: I've chosen to omit the ground truth of the action in the updated UI, since this data would not be available in a live situation.

## Demo

HARRY MAGUIRE vs Cesar Azpilicueta

![HARRY MAGUIRE](https://github.com/ghchen99/VARS/assets/56446026/8cdb8a88-c19d-4fdc-b754-3d2872dff9bc)

The AI Video Assistant Referee System assesses the provided clip and generates the two most likely decisions, along with their respective confidence scores. Unfortunately, due to GitHub's limitations on GIF size, discerning the AI prediction on the right may be challenging.

* The AI model expresses a confidence level of 45% in categorizing the incident as 'no foul.'
* Additionally, it indicates a 41% confidence in labeling the incident as a 'foul but no card.'

Recalling the incident from the 2020/21 season, it was ultimately deemed a 'no foul' by the referee, Martin Atkinson, and later confirmed by the VAR system. It's essential to note that this confirmation doesn't necessarily validate the system's efficacy but underscores the nuanced distinction between awarding or not awarding a penalty, as evident in this case with a mere 4% difference.

To assist referees in their decision-making, the model can identify specific offenses for consideration. In this instance, it highlights a 55% likelihood of elbowing and a 20% likelihood of pushing. Interestingly, the model's training data may not have included scenarios involving chokeholds, as evidenced by the absence of relevant information.


## SoccerNet-MVFouls

Follow the [link](https://pypi.org/project/SoccerNet/) to easily download the SoccerNet pip package.

If you want to download the data and annotations, you will need to fill a [NDA](https://docs.google.com/forms/d/e/1FAIpQLSfYFqjZNm4IgwGnyJXDPk2Ko_lZcbVtYX73w5lf6din5nxfmA/viewform) to get the password.

Then use the API to downlaod the data:

```
from SoccerNet.Downloader import SoccerNetDownloader as SNdl
mySNdl = SNdl(LocalDirectory="path/to/SoccerNet")
mySNdl.downloadDataTask(task="mvfouls", split=["train","valid","test","challenge"], password="enter password")
```
The dataset will be available at 720p soon!

The dataset consists of 3901 available actions. Each action is composed of at least two videos depicting the live action and at least one replay. 
The dataset is divided into a training set (2916 actions), validation set (411 actions), test set (301 actions) and challenge set (273 actions without the annotations).

The actions are annotated with 10 different properties describing the characteristics of the foul from a referee
perspective (e.g. the severity of the foul, the type of foul,
etc.). \
To ensure high-quality annotations, all these properties were manually annotated by a professional soccer referee with 6 years of experience and more than 300 official
games.

## VARS

Run the following lines to install all the dependencies:
```
conda create -n vars python=3.9

conda activate vars

conda install pytorch torchvision cudatoolkit=11.7 -c pytorch -c conda-forge

pip install -r requirements.txt
```

To start the training, run the following command:

```
python main.py --path "path/to/dataset" 
```

## VARS interface

<img width="1666" alt="Screenshot 2024-01-01 at 16 53 37" src="https://github.com/ghchen99/VARS/assets/56446026/52d51fd0-771d-4147-9912-7bb87cf15cb6">

Run the following lines to instal all the dependencies
```
conda create -n vars python=3.9

conda activate vars

pip install git+https://github.com/ajhamdi/mvtorch

pip install -r requirements.txt
```
Download the weights of the model: https://drive.google.com/drive/folders/1N0Lv-lcpW8w34_iySc7pnlQ6eFMSDvXn?usp=share_link

And save the 8_model.pth.tar file in the folder "interface".

Once the environment is ready, you can simply run the interface with the following command:
```
python main.py
```
Then select one or several clips in the folder "Dataset".


## License
See the [License](LICENSE) file for details.

## Citation

For further information check out Jan's [paper](https://arxiv.org/abs/2304.04617) and supplementary material.

Please cite their work if you use their dataset or code:
```
@InProceedings{Held2023VARS,
    author    = {Held, Jan and Cioppa, Anthony and Giancola, Silvio and Hamdi, Abdullah and Ghanem, Bernard and Van Droogenbroeck, Marc},
    title     = {{VARS}: Video Assistant Referee System for Automated Soccer Decision Making From Multiple Views},
    booktitle = cvsports,
    month     = Jun,
    year      = {2023},
	publisher = ieee,
	address = seattle,
    pages     = {5085-5096}
}
```

# Dataset for historical catalogs OCR

The Artl@s project focus on the global circulation of images from the 1890s to the advent of the Internet, using digital methodologies. Among its projects, BasArt is an online database of exhibition catalogs from the 19th and 20th centuries. 
In order to broaden this database, Caroline Corbières, intern of the project in 2020, worked on the automatisation of its process. A scanned exhibition catalog is taken as an input and then encoded in XML-TEI and structured in csv. 

In this context, the aim of this repository is to improve the ocerization of this [Catalogs Workflow](https://github.com/carolinecorbieres/ArtlasCatalogues). This step occurs at the beginning of the workflow and transforms the data from an image to a text. 
The idea was not only to refine the OCR for [Artl@s](https://artlas.huma-num.fr/fr/) but also to make a useful tool for researchers who need to ocerize their catalogues. Therefore, this dataset holds exhibition catalogs, prepared by Caroline Corbières, catalogs of 19th to nowadays manuscripts fairs of the [Katabase](https://github.com/katabase) project, arranged by Simon Gabay and owners directories from the [Adresses et Annuaires group](https://paris-timemachine.huma-num.fr/groupe-adresses-et-annuaires/) of Paris Time Machine of the EHESS, produced by Gabriela Elgarrista. 

The first dataset is composed of 30 pages from the 150 pages dataset prepared [here](https://github.com/Juliettejns/cataloguesSegmentationOCR/), with 10 pages of each type of documents. It is supposed to be a small representative dataset in order to have a look on the impact of repolygonization, which is a process of optimizing the lines' polygones and ensuring the documents presented are compatible with the Kraken OCR, on the OCR. 90% of the dataset is used for the training and 10% for its evaluation. Therefore, the dev dataset is composed of 3 pages, with each page from a different type of document, selected randomly in the dataset.

After this test, a second dataset has been created. It is composed of 100 pages from the 150 pages dataset, with 50 pages of each type of documents. A second model has been trained from this dataset, without repolygonisation, due to the results of the first model. The train and dev dataset have been created using the random_data python script which randomly select the differents pages of the corpus. 90% of the dataset is used for the training and 10% for its evaluation.

## Repository
```
├── Dataset30
|     ├── train
|     │     ├─ images
|     |     └─ transcription in Alto4 XML
|     └─  dev
|           ├─ images
|           └─ transcription in Alto4 XML
│ 
├── Dataset100
|     ├─ images
|     └─ transcription in Alto4 XML
|
├── Models
|     ├─ model_best_30.mlmodel
|     ├─ model_best_repolygonize_30.mlmodel
|     └─ model_best_100.mlmodel
|
├── Images
|
├── Dataset30.csv
├── Dataset100.csv
├── random_data.py
└─ README.md
```

## Commands
In order to recreate the models presented in this repository, here are the commands done. 
- Install Kraken by following instructions [here](https://github.com/mittagessen/kraken).
- Clone this repository: `git clone https://github.com/Juliettejns/cataloguesOCR/`
- For the Dataset30:
    - Train model without repolygonization: `ketos train -t train/*.xml -e dev/*.xml -u NFKD -f alto`
    - Train model with repolygonization: `ketos train -t train/*.xml -e dev/*.xml -u NFKD -f alto --repolygonize`
- For the Dataset100:
    - Create a new dev dataset: `random_data.py Dataset100/*.xml`
    - Train model: `ketos train -t train.txt -e dev.txt -u NFKD -f alto`
- Evaluate models: `ketos test -m [MODEL_NAME] -e [EVAL_DIRECTORY]/*.xml -f alto`

## Results
<p class="float" align="center">
 <img src="images/resultat_model_30.png" height="200" width="300"/>
 <img src="images/resultats_model_repolygonize_30.png" height="200" width="300"/>
</p>
Evaluation on the dev/ dataset:</br>
Left: results for the model of 30 pages without repolygonization.</br>
Right: results for the model of 30 pages with repolygonization.</br>
</br>

<p align="center">
    <img src="images/results_model_100.png" height="200" width="300"/>
    <img src="images/resultats_model_100_dev.png" height="200" width="300"/>
</p>
Results for the model of 100 pages without repolygonization:</br>
Left: evaluation on the dev dataset from the 100 pages.</br>
Right: evaluation on the dev/ dataset of the 30 pages.</br>


## Thanks to 
Thanks to Simon Gabay, Claire Jahan, Caroline Corbières, Gabriela Elgarrista and Carmen Brando for their help and work.

## Credits
This repository is developed by Juliette Janes, intern of the [Artl@s](https://artlas.huma-num.fr/fr/) project, with the help of Simon Gabay under the supervision of Béatrice Joyeux-Prunel.
 - Manuscripts' catalogs preparation has been done by Simon Gabay.
 - Exhibitions' catalogs preparation has been done by Caroline Corbières. 
 - Annuaires preparation has been done by Gabriela Elgarrista, under the supervision of Carmen Brando.

## Licence
Images from catalogs published prior 1920 and transcriptions are CC-BY. </br>
The other images are extracts of catalogs published after 1920 and are the intellectual property of their productor.</br>
![68747470733a2f2f692e6372656174697665636f6d6d6f6e732e6f72672f6c2f62792f322e302f38387833312e706e67](https://user-images.githubusercontent.com/56683417/115525743-a78d2400-a28f-11eb-8e45-4b6e3265a527.png)

## Cite this repository
Juliette Janes, Simon Gabay, Béatrice Joyeux-Prunel, _Dataset for Historical Catalogs OCR_, 2021, Paris: ENS Paris https://github.com/Juliettejns/cataloguesOCR/

## Contacts
If you have any questions or remarks, please contact juliette.janes@chartes.psl.eu and simon.gabay@unige.ch.

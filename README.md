# BERN2

We present **BERN2** (Advanced **B**iomedical **E**ntity **R**ecognition and **N**ormalization), a tool that improves the previous neural network-based NER tool by employing a multi-task NER model and neural network-based NEN models to achieve much faster and more accurate inference. This repository provides a way to host your own BERN2 server. See our [paper](https://arxiv.org/abs/2201.02080) for more details.

***** **Try BERN2 at [http://bern2.korea.ac.kr](http://bern2.korea.ac.kr)** ***** 

## Installing BERN2

You first need to install BERN2 and its dependencies.

```bash
# Install torch with conda (please check your CUDA version)
conda create -n bern2 python=3.7
conda activate bern2
conda install pytorch==1.9.0 cudatoolkit=10.2 -c pytorch
conda install faiss-gpu libfaiss-avx2 -c conda-forge

# Check if cuda is available
python -c "import torch;print(torch.cuda.is_available())"

# Install BERN2
git clone git@github.com:dmis-lab/BERN2.git
cd BERN2
pip install -r requirements.txt

```

(Optional) If you want to use mongodb as a caching database, you need to install and run it.
```
# https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition-using-deb-packages
sudo systemctl start mongod
sudo systemctl status mongod
```

Then, you need to download resources (e.g., external modules or dictionaries) for running BERN2. Note that you will need 70GB of free disk space.

```
wget http://nlp.dmis.korea.edu/projects/bern2/resources.tar.gz
tar -zxvf resources.tar.gz
rm -rf resources.tar.gz
# install CRF
cd resources/GNormPlusJava/CRF
./configure --prefix="$HOME"
make
make install
cd ../../..
```

## Running BERN2

The following command runs BERN2.
```
export CUDA_VISIBLE_DEVICES=0
cd scripts
bash run_bern2.sh
```

(Optional) To restart BERN2, you need to run the following commands.
```
export CUDA_VISIBLE_DEVICES=0
cd scripts
bash stop_bern2.sh
bash start_bern2.sh
```

## Annotations

Click [here](http://nlp.dmis.korea.edu/projects/bern2/annotations/anntation_v1.1.tar.gz) to download the annotations (NER and normalization) for 25.7+ millions of PubMed articles (From pubmed21n0001 to pubmed21n1057 (2021.01.12)) (Compressed, 18 GB).

The data provided by BERN2 is post-processed and may differ from the most current/accurate data available from [U.S. National Library of Medicine (NLM)](https://www.nlm.nih.gov/).

## Citation
```bibtex
@article{sung2022bern2,
    title={BERN2: an advanced neural biomedical namedentity recognition and normalization tool}, 
    author={Sung, Mujeen and Jeong, Minbyul and Choi, Yonghwa and Kim, Donghyeon and Lee, Jinhyuk and Kang, Jaewoo},
    year={2022},
    eprint={2201.02080},
    archivePrefix={arXiv},
    primaryClass={cs.CL}
}
```

## Contact Information
For help or issues using BERN2, please submit a GitHub issue. Please contact Mujeen Sung (`mujeensung (at) korea.ac.kr`), or Minbyul Jeong (`minbyuljeong (at) korea.ac.kr`) for communication related to BERN2.

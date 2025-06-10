## Getting Started with Project Structure
1) create a new repo (github + dagshub)
2) cp + ps (from dagshub Track your code)
3) Folder:-
    ->data
        raw 
        processed
    ->src:
        __init__.py
        evaluate.py
        preprosess.py
        train.py
    ->params.yaml
4) params.yamal
preprocess:
    input:data/raw/data.csv
    output: data/processed/data.csv
train:
    data: data/processed/data.csv
    model: models/model.pkl
    random_state:42
    n_estimators:100
    max_depth:5
5) preprocessing.py
6) trina.pyng 
    After importing the library -> dagshub > remote > Experiments > MLFlow Tracking Remote(cp)
    os.environment['MLFLOW_TRACKING_URI']= "paste"
    os.environment['MLFLOW_TRACKING_USERNAME']="SadabAli"
    os.environment['MLFLOW_TRACKING_PASSWORD']="Dagshub > data(DVC) > Setup Credential > secrate_access_key"
7) evaluate.py
    os.environment['MLFLOW_TRACKING_URI']= "paste"
    os.environment['MLFLOW_TRACKING_USERNAME']="SadabAli"
    os.environment['MLFLOW_TRACKING_PASSWORD']="Dagshub > data(DVC) > Setup Credential > secrate_access_key" 
8) open new terminal
    dvc init 
    dvc add data/raw/data.csv
    To track the changes with git, run:
        cp +ps
    git commit -m "Add raw data"
9) pipeline
open git bash
    dvc stage add -n preprocess
    -p preprocess.input,preprocess.output
    -d src/preprocess.py -d data/raw/data.csv
    -o data/processed/data.csv
    python src/preprocess.py

    dvc stage add -n train
    -p train.data,train.model,train.random_state,train.n_estimators,train.max_depth
    -d src/train.py -d data/raw/data.csv
    -o models/model.pkl
    python src/train.py

    dvc stage add -n evaluate
    -d src/evaluate.py -d models/model.pkl -d data/raw/data.csv
    python src/evaluate.py

10) dvc repro
11) daghub > remote > Data(DVC) > Add a Dagshub DVC remote(cp + ps)
    daghub > remote > Data(DVC) > Setup the credential
    dvc pull -r origin
    dvc push -r origin
12) cmd:
    git add .
    git commit -m "final commit"
    git push origin main
# TFX Vitals Pipeline

Details here: https://www.tensorflow.org/tfx/guide/build_local_pipeline

Working under tfx_keras_component_on_ocp/vitals_septic directory

TFX makes it easier to orchestrate your machine learning (ML) workflow as a pipeline, in order to:

1. Automate your ML process, which lets you regularly retrain, evaluate, and deploy your model.
1. Create ML pipelines which include deep analysis of model performance and validation of newly trained models to ensure performance and reliability.
1. Monitor training data for anomalies and eliminate training-serving skew
1. Increase the velocity of experimentation by running a pipeline with different sets of hyperparameters.
A typical pipeline development process begins on a local machine, with data analysis and component setup, before being deployed into production.


1. List available templates
'tfx template list'

2. Build using a template
This will create 3x-directories data, models and pipeline; 2x-notebooks data_validation and model_analysis; 4x-python files __init__, kubeflow_runner, kubeflow_v2_runner, local_runner
'''
tfx template copy --model=taxi --pipeline_name=vitals-pipeline --destination_path=./

# Replace the following:
# template: The name of the template you want to copy.
# pipeline-name: The name of the pipeline to create.
# destination-path: The path to copy the template into.

A pipeline directory with
- pipeline.py - defines the pipeline, and lists which components are being used
- configs.py - hold configuration details such as where the data is coming from or which orchestrator is being used

A data directory
- This typically contains a data.csv file, which is the default source for ExampleGen. You can change the data source in configs.py.

A models directory with preprocessing code and model implementations

The template copies DAG runners for local environment and Kubeflow.

Some templates also include Python Notebooks so that you can explore your data and artifacts with Machine Learning MetaData.
'''

3. Run the following in your pipeline directory
'''
tfx run create --pipeline_name vitals_pipeline
tfx pipeline create --pipeline_path local_runner.py
'''


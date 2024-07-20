# Exploratory Data Analysis using Bigquery and Workbench


## Overview


In this lab you learn the process of analyzing a dataset stored in BigQuery using a Workbench Instance notebook to perform queries and present the data using various statistical plotting techniques. The analysis will help you discover patterns in the data.

### Learning objectives

* Create a Workbench Instance Notebook
* Connect to BigQuery datasets
* Perform statistical analysis on a Pandas Dataframe
* Create Seaborn plots for Exploratory Data Analysis in Python
* Write a SQL query to pick up specific fields from a BigQuery dataset


Vertex AI is a unified platform for building, deploying, and managing machine learning (ML) applications.

Vertex AI Workbench notebooks provide a flexible and scalable solution for developing and deploying ML models on Google Cloud. Choose Workbench if you need more customization options and need complete control over your machine learning environment. It offers the security and compliance features needed for enterprise organizations and integrates with other Google Cloud services like Vertex AI and BigQuery for an enhanced data science and machine learning workflow.

BigQuery is a powerful, fully managed, serverless data warehouse that allows you to analyze and manage large datasets with ease. BigQuery uses a familiar standard SQL dialect, making it easy for analysts and data scientists to use without needing to learn a new language.

Vertex AI offers two Notebook Solutions, Workbench and Colab Enterprise.

![Colab](img/colab1.png)

### Workbench

Vertex AI Workbench is a good option for projects that prioritize control and customizability. It’s great for complex projects spanning multiple files, with complex dependencies. It’s also a good choice for a data scientist who is transitioning to the cloud from a workstation or laptop.

Vertex AI Workbench Instances comes with a preinstalled suite of deep learning packages, including support for the TensorFlow and PyTorch frameworks.

![workbench1](img/workbench1.png)


## Set up your Qwiklabs environments

### Qwiklabs setup

![[/fragments/start-qwiklab]]



## Task 1. Set up your environment

1. Enable the Vertex AI API

Navigate to the [Vertex AI section of your Cloud Console](https://console.cloud.google.com/ai/platform?utm_source=codelabs&utm_medium=et&utm_campaign=CDR_sar_aiml_vertexio_&utm_content=-) and click __Enable All Recommended APIs__.

## Task 2. Create a Workbench Notebook

1. In the Vertex AI section, scroll down to __Notebooks__. Click __Workbench__.

![select_workbench](img/select_workbench.png)

2. At the top of the workspace, make sure __INSTANCES__ is selected.

3. Click __CREATE NEW__.

![create_wbnb](img/create_wbnb.png)

A new instance window appears (as shown below)

4. For this lab, name the instance and select __CREATE__.
If you want more control, you can select __ADVANCED OPTIONS__. Once you name the instance, and select __CREATE__, you assume all default environment settings  .

![wb_new_instance_window](img/wb_new_instance_window.png)

You will notice your new instance spinning up in the __Instance Name__ section.


A green check appears next to the instance when it is ready to be use.

![my-new-instance](img/my-new-instance.png)

5. Click __OPEN JUPYTERLAB__ to open a Jupyter notebook.

![open_jupyterlab](img/open_jupyterlab.png)

6. To launch Python 3 Jupyter Notebook, click the __Python 3__ notebook.

![launch_wb_nb](img/launch_wb_nb.png)

7. Once the notebook is launched, rename it by right-clicking on the __untitled.ipynb__ file in the menu bar and selecting __Rename Notebook__.

![rename_wbnb](img/rename_wbnb.png)
![my-notebook2](img/my-notebook2.png)


## Task 3. Clone a repo within your Vertex AI Notebook instance

The GitHub repo contains both the lab file and solutions files for the course.

1. To clone the training-data-analyst notebook in your JupyterLab instance, copy this code into the first cell in the notebook.

```
!git clone https://github.com/GoogleCloudPlatform/training-data-analyst
```
Output shown.
![git_ouput](img/git_ouput.png)


2. Confirm that you have cloned the repository. Double-click on the __training-data-analyst__ directory and ensure that you can see its contents.

![confirm_training-data-analyst](img/confirm_training-data-analyst.png)

1. In the notebook interface, navigate to __training-data-analyst > courses > machine_learning > deepdive2 > launching_into_ml > solutions__ and open __workbench_explore_bq.ipynb__.

2. Carefully read through the notebook instructions.

![Alt text](img/workbench_explore_bq_nb.png)



## Congratulations!

In this lab you learned how to:

* Create a Workbench Instance Notebook
* Clone a GitHub repository
* Connect to a BigQuery dataset
* Perform statistical analysis on a Pandas Dataframe
* Create Seaborn plots for Exploratory Data Analysis in Python
* Write a SQL query to pick up specific fields from a BigQuery dataset.


![[/fragments/endqwiklab]]


**Manual Last Updated: December 14, 2023**

**Lab Last Tested: December 14, 2023**

![[/fragments/copyright]]

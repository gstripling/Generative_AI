\<h1\>Orchestrate ML Workflows with the Data Science Agent in Vertex AI\</h1\>  
\<h2\>GSP1321\</h2\>  
\<p\>\<img alt="Google Cloud self-paced labs logo" src="https://cdn.qwiklabs.com/GMOHykaqmlTHiqEeQXTySaMXYPHeIvaqa2qHEzw6Occ%3D"\>\</p\>  
\<h2\>Overview\</h2\>  
\<p\>\<a href="https://cloud.google.com/vertex-ai/docs/colab-enterprise/introduction"\>Colab Enterprise\</a\> in Vertex AI now features a powerful \<strong\>Data Science Agent\</strong\>. This intelligent coding partner accelerates the entire data-to-model lifecycle by helping you plan workflows, generate complex code, visualize data, and troubleshoot errors. While it excels at exploratory analysis, its ability to understand context and generate framework-specific code makes it an invaluable tool for orchestrating Machine Learning (ML) workflows.\</p\>  
\<p\>In this lab, you will leverage the Data Science Agent to automate the creation of a machine learning pipeline. Traditionally, defining components and pipelines in the Kubeflow Pipelines (KFP) SDK requires writing significant boilerplate code. You will see how the Data Science Agent can convert natural language intent into production-ready pipeline code, allowing you to move from concept to orchestration in minutes.\</p\>  
\<h3\>Business use-case\</h3\>  
\<p\>Cymbal Foods needs to modernize its predictive maintenance systems for its distribution centers. The data science team wants to retrain their models weekly on the latest sensor data. However, the team is bottlenecked by the complexity of writing and maintaining the orchestration code required for Vertex AI Pipelines. By adopting the Data Science Agent in Vertex AI, Cymbal Foods aims to empower its data scientists to define, deploy, and debug these pipelines using natural language, significantly reducing time-to-production.\</p\>  
\<h2\>Objectives\</h2\>  
\<p\>In this lab, you learn how to:\</p\>  
\<ul\>  
\<li\>Enable and access the Data Science Agent in Vertex AI Colab Enterprise.\</li\>  
\<li\>Use the agent to perform exploratory data analysis (EDA) on a dataset.\</li\>  
\<li\>Prompt the agent to generate Kubeflow Pipelines (KFP) components for data training.\</li\>  
\<li\>Use the agent to stitch components into a complete compiled pipeline.\</li\>  
\<li\>Submit and monitor the pipeline run in Vertex AI Pipelines.\</li\>  
\</ul\>  
\<h2\>Setup and requirements\</h2\>  
\<h3\>Before you click the Start Lab button\</h3\>  
\<p\>Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click \<strong\>Start Lab\</strong\>, shows how long Google Cloud resources are made available to you.\</p\>  
\<p\>This hands-on lab lets you do the lab activities in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials you use to sign in and access Google Cloud for the duration of the lab.\</p\>  
\<p\>To complete this lab, you need:\</p\>  
\<ul\>  
\<li\>Access to a standard internet browser (Chrome browser recommended).\</li\>  
\</ul\>  
\<ql-warningbox\>  
\<strong\>Note:\</strong\> Use an Incognito (recommended) or private browser window to run this lab. This prevents conflicts between your personal account and the student account, which may cause extra charges incurred to your personal account.  
\</ql-warningbox\>  
\<ul\>  
\<li\>Time to complete the lab—remember, once you start, you cannot pause a lab.\</li\>  
\</ul\>  
\<ql-warningbox\>  
\<strong\>Note:\</strong\> Use only the student account for this lab. If you use a different Google Cloud account, you may incur charges to that account.  
\</ql-warningbox\>  
\<h3\>How to start your lab and sign in to the Google Cloud console\</h3\>  
\<ol\>  
\<li\>  
\<p\>Click the \<strong\>Start Lab\</strong\> button. If you need to pay for the lab, a dialog opens for you to select your payment method.  
On the left is the Lab Details pane with the following:\</p\>  
\<ul\>  
\<li\>The Open Google Cloud console button\</li\>  
\<li\>Time remaining\</li\>  
\<li\>The temporary credentials that you must use for this lab\</li\>  
\<li\>Other information, if needed, to step through this lab\</li\>  
\</ul\>  
\</li\>  
\<li\>  
\<p\>Click \<strong\>Open Google Cloud console\</strong\> (or right-click and select \<strong\>Open Link in Incognito Window\</strong\> if you are running the Chrome browser).\</p\>  
\<p\>The lab spins up resources, and then opens another tab that shows the Sign in page.\</p\>  
\<p\>\<strong\>\<em\>Tip:\</em\>\</strong\> Arrange the tabs in separate windows, side-by-side.\</p\>  
\<ql-infobox\>  
\<strong\>Note: \</strong\>If you see the \<strong\>Choose an account\</strong\> dialog, click \<strong\>Use Another Account\</strong\>.  
\</ql-infobox\>

\</li\>

\<li\>

\<p\>If necessary, copy the \<strong\>Username\</strong\> below and paste it into the \<strong\>Sign in\</strong\> dialog.\</p\>

\<ql-code-block bash="" nowrap templated=""\>

{{{user\_0.username | "Username"}}}  
\</ql-code-block\>  
\<p\>You can also find the Username in the Lab Details pane.\</p\>  
\</li\>  
\<li\>  
\<p\>Click \<strong\>Next\</strong\>.\</p\>  
\</li\>  
\<li\>  
\<p\>Copy the \<strong\>Password\</strong\> below and paste it into the \<strong\>Welcome\</strong\> dialog.\</p\>  
\<ql-code-block bash="" nowrap templated=""\>  
{{{user\_0.password | "Password"}}}  
\</ql-code-block\>  
\<p\>You can also find the Password in the Lab Details pane.\</p\>  
\</li\>  
\<li\>  
\<p\>Click \<strong\>Next\</strong\>.\</p\>  
\<ql-infobox\>  
\<strong\>Important: \</strong\>You must use the credentials the lab provides you. Do not use your Google Cloud account credentials.  
\</ql-infobox\>  
\<ql-warningbox\>  
\<strong\>Note: \</strong\>Using your own Google Cloud account for this lab may incur extra charges.  
\</ql-warningbox\>  
\</li\>  
\<li\>  
\<p\>Click through the subsequent pages:\</p\>  
\<ul\>  
\<li\>Accept the terms and conditions.\</li\>  
\<li\>Do not add recovery options or two-factor authentication (because this is a temporary account).\</li\>  
\<li\>Do not sign up for free trials.\</li\>  
\</ul\>  
\</li\>  
\</ol\>  
\<p\>After a few moments, the Google Cloud console opens in this tab.\</p\>  
\<ql-infobox\>  
\<strong\>Note:\</strong\> To access Google Cloud products and services, click the \<strong\>Navigation menu\</strong\> or type the service or product name in the \<strong\>Search\</strong\> field.  
\<img alt="Navigation menu icon and Search field" src="https://cdn.qwiklabs.com/9Fk8NYFp3quE9mF%2FilWF6%2FlXY9OUBi3UWtb2Ne4uXNU%3D"\>  
\</ql-infobox\>  
\<h2\>Task 1\. Set up the Data Science Agent environment\</h2\>  
\<p\>In this task, you will enable the necessary APIs and initialize a Colab Enterprise notebook where the Data Science Agent resides.\</p\>  
\<ol\>  
\<li\>  
\<p\>In the Google Cloud Console, use the search bar to find and select \<strong\>Vertex AI\</strong\>.\</p\>  
\</li\>  
\<li\>  
\<p\>From the Vertex AI dashboard, click \<strong\>Enable All Recommended APIs\</strong\> if prompted.\</p\>  
\</li\>  
\<li\>  
\<p\>In the left-hand navigation menu, under \<strong\>Notebooks\</strong\>, select \<strong\>Colab Enterprise\</strong\>.\</p\>  
\</li\>  
\<li\>  
\<p\>Click \<strong\>Create Notebook\</strong\> to create a new notebook file. You do not need to create a runtime template yet; the default one will be sufficient for this lab.\</p\>  
\</li\>  
\<li\>  
\<p\>Once the notebook loads, locate the \<strong\>Gemini\</strong\> button (often a sparkle icon) in the top-right or sidebar of the interface. This opens the Data Science Agent chat interface.\</p\>  
\</li\>  
\</ol\>  
\<p\>\</p\>  
\<ol start="6"\>  
\<li\>  
\<p\>Connect to a runtime by clicking \<strong\>Connect\</strong\> in the top right corner. Select \<strong\>Create new runtime\</strong\>, keep the default settings (e.g., Python 3, standard machine type), and click \<strong\>Create\</strong\>.\</p\>  
\</li\>  
\</ol\>  
\<ql-infobox\>  
\<b\>Note:\</b\> It may take 2-3 minutes for the runtime to provision. While you wait, you can familiarize yourself with the agent interface.  
\</ql-infobox\>  
\<p\>Click \<strong\>Check my progress\</strong\> to verify the objective.  
\<ql-activity-tracking step="1"\>  
Enable Vertex AI and create a Colab Enterprise notebook.  
\</ql-activity-tracking\>\</p\>  
\<h2\>Task 2\. Accelerate EDA with the Agent\</h2\>  
\<p\>Before building a pipeline, data scientists typically explore their data. The Data Science Agent can instantly generate code to load and visualize datasets, saving you from remembering pandas syntax.\</p\>  
\<ol\>  
\<li\>  
\<p\>In the Data Science Agent chat pane, enter the following prompt:\</p\>  
\</li\>  
\</ol\>  
\<ql-code-block language="plaintext"\>  
I want to use the 'bigquery-public-data.ml\_datasets.penguins' dataset. Please write Python code to load this data from BigQuery into a dataframe and display the first 5 rows.  
\</ql-code-block\>  
\<ol start="2"\>  
\<li\>  
\<p\>The agent will generate a code block. Click \<strong\>Insert\</strong\> to add it to your notebook, then run the cell.\</p\>  
\</li\>  
\<li\>  
\<p\>Now, ask for a visualization:\</p\>  
\</li\>  
\</ol\>  
\<ql-code-block language="plaintext"\>  
Generate code to visualize the distribution of 'body\_mass\_g' broken down by 'species' using a histogram.  
\</ql-code-block\>  
\<ol start="4"\>  
\<li\>  
\<p\>Insert and run the code. Notice how the agent correctly identified the relevant libraries (like matplotlib or seaborn) and column names without you explicitly specifying them.\</p\>  
\</li\>  
\</ol\>  
\<p\>\</p\>  
\<p\>Click \<strong\>Check my progress\</strong\> to verify the objective.  
\<ql-activity-tracking step="2"\>  
Load and visualize data using Agent-generated code.  
\</ql-activity-tracking\>\</p\>  
\<h2\>Task 3\. Generate KFP Components with the Agent\</h2\>  
\<p\>Writing Kubeflow Pipelines (KFP) components often involves complex syntax for decorators, type hinting, and package imports. You will now use the Data Science Agent to generate this boilerplate code for you.\</p\>  
\<ol\>  
\<li\>  
\<p\>In the chat pane, tell the agent you are shifting to pipeline development:\</p\>  
\</li\>  
\</ol\>  
\<ql-code-block language="plaintext"\>  
I want to build a Vertex AI Pipeline. First, please install the google-cloud-pipeline-components and kfp packages.  
\</ql-code-block\>  
\<ol start="2"\>  
\<li\>  
\<p\>Insert and run the installation code. You may need to restart the kernel if prompted.\</p\>  
\</li\>  
\<li\>  
\<p\>Now, ask the agent to create a training component. Copy and paste the prompt below:\</p\>  
\</li\>  
\</ol\>  
\<ql-code-block language="plaintext"\>  
Create a KFP component named 'train\_model' using the @component decorator.  
It should take a BigQuery source string as input.  
Inside the component:

1. Load the penguins data from the BigQuery source.  
2. Drop rows with null values.  
3. Train a Scikit-learn DecisionTreeClassifier to predict 'species'.  
4. Print the model accuracy.  
   Use 'pandas', 'scikit-learn', and 'google-cloud-bigquery' as base packages.  
   \</ql-code-block\>  
   \<ol start="4"\>  
   \<li\>  
   \<p\>Review the generated code. The agent should have produced a function decorated with \<code\>@component\</code\>, including the necessary imports \<em\>inside\</em\> the function scope (a requirement for KFP components).\</p\>  
   \</li\>  
   \<li\>  
   \<p\>\<strong\>Insert\</strong\> and \<strong\>Run\</strong\> the cell to define the component.\</p\>  
   \</li\>  
   \</ol\>  
   \<ql-infobox\>  
   \<b\>Tip:\</b\> If the Agent missed adding the packages\_to\_install parameter in the decorator, you can simply ask it: "Please update the code to include pandas and scikit-learn in the packages\_to\_install argument."  
   \</ql-infobox\>

\<h2\>Task 4\. Orchestrate and Submit the Pipeline\</h2\>  
\<p\>Now that you have a component, you need to define the pipeline structure and submit it to Vertex AI. This requires a compiler and a pipeline job definition.\</p\>  
\<ol\>  
\<li\>  
\<p\>Ask the agent to stitch it together:\</p\>  
\</li\>  
\</ol\>  
\<ql-code-block language="plaintext"\>  
Now, write the code to define a pipeline named 'penguin-training-pipeline' that uses the 'train\_model' component.  
Then, compile this pipeline to a file named 'pipeline.json'.  
Finally, submit this pipeline run to Vertex AI Pipelines using a temporary bucket for staging.  
\</ql-code-block\>  
\<ol start="2"\>  
\<li\>  
\<p\>The Agent will generate a block of code that:\</p\>  
\<ul\>  
\<li\>Defines a function decorated with \<code\>@dsl.pipeline\</code\>.\</li\>  
\<li\>Uses \<code\>kfp.compiler.Compiler\</code\>.\</li\>  
\<li\>Uses \<code\>aiplatform.PipelineJob\</code\>.\</li\>  
\</ul\>  
\</li\>  
\<li\>  
\<p\>\<strong\>Important:\</strong\> You may need to replace placeholders in the generated code (like \<code\>PROJECT\_ID\</code\> or \<code\>STAGING\_BUCKET\</code\>) with your actual lab details.\</p\>  
\<ul\>  
\<li\>\<strong\>Project ID:\</strong\> \<ql-variable key="project\_0.startup\_script.project\_id" placeholder="Project ID"\>\</ql-variable\>\</li\>  
\<li\>\<strong\>Region:\</strong\> \<ql-variable key="project\_0.startup\_script.region" placeholder="Region"\>\</ql-variable\>\</li\>  
\<li\>\<strong\>Bucket:\</strong\> \<ql-variable key="project\_0.startup\_script.project\_id" placeholder="GCS Bucket"\>\</ql-variable\> (The lab pre-provisions a bucket with your project ID).\</li\>  
\</ul\>  
\</li\>  
\<li\>  
\<p\>Insert the code, update the placeholders, and run the cell.\</p\>  
\</li\>  
\<li\>  
\<p\>Once the cell runs successfully, it will output a link to the \<strong\>Vertex AI Pipelines\</strong\> dashboard.\</p\>  
\</li\>  
\</ol\>  
\<p\>\</p\>  
\<p\>Click \<strong\>Check my progress\</strong\> to verify the objective.  
\<ql-activity-tracking step="3"\>  
Compile and submit a Vertex AI Pipeline.  
\</ql-activity-tracking\>\</p\>  
\<h2\>Task 5\. Troubleshooting with the Agent\</h2\>  
\<p\>One of the Data Science Agent's strongest features is "Explain Error". If your pipeline fails or a cell errors out, the agent can diagnose the issue.\</p\>  
\<ol\>  
\<li\>  
\<p\>To demonstrate this, create a new code cell and intentionally write some broken code, for example:\</p\>  
\<ql-code-block language="python"\>  
import pandas as pd  
df \= pd.read\_csv("non\_existent\_file.csv")  
\</ql-code-block\>  
\</li\>  
\<li\>  
\<p\>Run the cell to trigger the error.\</p\>  
\</li\>  
\<li\>  
\<p\>Look for the \<strong\>Explain error\</strong\> button that appears next to the error output, or simply ask the agent in the chat pane: "Why did this fail?"\</p\>  
\</li\>  
\<li\>  
\<p\>The agent will analyze the traceback and explain that the file was not found, often suggesting how to fix the path or check for file existence.\</p\>  
\</li\>  
\</ol\>  
\<h2\>Congratulations\!\</h2\>  
\<p\>You have successfully used the Data Science Agent in Vertex AI to accelerate the creation of an ML workflow. You moved from raw data to a deployed pipeline without manually writing the heavy boilerplate code required for KFP, demonstrating how AI agents can act as powerful force multipliers for data science teams at companies like Cymbal Foods.\</p\>  
\<h3\>Next steps / learn more\</h3\>  
\<ul\>  
\<li\>\<a href="https://cloud.google.com/vertex-ai/docs/colab-enterprise/overview"\>Overview of Colab Enterprise\</a\>\</li\>  
\<li\>\<a href="https://cloud.google.com/vertex-ai/docs/pipelines/introduction"\>Vertex AI Pipelines Documentation\</a\>\</li\>  
\<li\>\<a href="https://cloud.google.com/gemini/docs/code/assist"\>Gemini Code Assist\</a\>\</li\>  
\</ul\>
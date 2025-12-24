# **Accelerate ML Workflows with the Data Science Agent**

## **GSPXXX**

## **Overview**

[Vertex AI Pipelines](https://cloud.google.com/vertex-ai/docs/pipelines/introduction) is a key tool for automating Machine Learning workflows. In this lab, you will act as a Data Scientist at **Cymbal Media**, a marketing agency.

Business Use Case:  
Cymbal Media runs advertising campaigns across four channels: Television, Social Media, Digital Ads, and Radio. They want to predict the resulting Sales based on the budget spent in these channels. To ensure their predictions remain accurate as new campaign data arrives, they need an automated ML pipeline that can ingest data, retrain a regression model, and evaluate its performance.

You will use the **Google Cloud Data Science Agent** in Colab Enterprise to create this pipeline. You will prompt the agent to ingest a public dataset, write the pipeline components, and deploy the workflow.

## **Objectives**

In this lab, you learn how to:

* Setup Colab Enterprise and the Data Science Agent.  
* Use the Google Cloud Data Science Agent in Colab Enterprise to generate, debug, and explain Python code for ML infrastructure.  
* Prompt the Agent to load and explore datasets directly from Cloud Storage.  
* Generate and compile Kubeflow Pipelines (KFP) components to orchestrate data loading, model training, and evaluation.  
* Enhance your pipeline with hyperparameter tuning for better performance and conditional logic to ensure only quality models are deployed.  
* Register successful models to the Vertex AI Model Registry, track run metrics using Vertex AI Experiments, and automate execution with Pipeline Schedules.

## **Setup and requirements**

### **Before you click the Start Lab button**

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click **Start Lab**, shows how long Google Cloud resources are made available to you.

**Note:** Use an Incognito (recommended) or private browser window to run this lab. This prevents conflicts between your personal account and the student account.

### **How to start your lab and sign in to the Google Cloud console**

1. Click the **Start Lab** button.  
2. Click **Open Google Cloud console** (or right-click and select **Open Link in Incognito Window**).  
3. Enter the **Username** and **Password** provided in the Lab Details pane.  
4. Accept the terms and conditions and skip recovery options.

## **Task 1\. Set up Colab Enterprise**

1. In the Google Cloud Console, navigate to **Vertex AI \> Colab Enterprise**.  
2. Click **\+ Create Notebook**.  
3. Rename the notebook to media\_sales\_pipeline.ipynb.  
4. **Connect to a Runtime:**  
   * Click **Connect** in the top right.  
   * Select **Create new runtime**.  
   * Keep defaults (Python 3\) and click **Create**.  
5. Open the **Data Science Agent** chat interface (click the sparkle icon ✨ or "Gemini" in the sidebar).

## **Task 2\. Explore the Dataset**

We will start by loading the data from a public Cloud Storage bucket to understand its structure before building the pipeline.

1. In the **Data Science Agent** chat, enter the following prompt:  
   Plaintext  
   I need to explore a dataset located at this URL:  
   https://storage.googleapis.com/my-datasets-gs/media\_sales\_cymbal.csv

   Write code to:  
   1\. Load this CSV file directly into a pandas DataFrame.  
   2\. Display the first 5 rows.  
   3\. Print the column names and data types.

2. **Select an Action:**  
   * Click **Accept and Run** to insert the code into the notebook and execute it immediately.  
   * Alternatively, click **Accept** to just insert the code, or **Cancel** if you want to refine your prompt.  
3. **Review Output:** You should see columns for tv, social, digital, radio (features) and sales (target).

## **Task 3\. Generate Pipeline Components**

Now we will ask the agent to write the distinct steps of our ML pipeline.

### **Component 1: Load Data**

1. Enter the prompt:  
   Plaintext  
   I want to start building a Vertex AI Pipeline.  
   Write a KFP v2 component (\`@component\`) named \`load\_data\`.  
   It should:  
   1\. Take a \`data\_url\` string as input.  
   2\. Read the CSV from that URL into a pandas DataFrame (using pandas directly).  
   3\. Split the data into training (80%) and testing (20%) sets.  
   4\. Output two \`dataset\` artifacts: \`train\_data\` and \`test\_data\`.  
   5\. Use base image \`python:3.9\` and install \`pandas\` and \`scikit-learn\`.

2. **Review and Execute:** Review the generated code. Click **Accept and Run** (or **Accept**, then run manually). If the code looks incorrect, click **Cancel** and re-prompt.

### **Component 2: Train Model**

1. Enter the prompt:  
   Plaintext  
   Write a second component named \`train\_model\`.  
   It should:  
   1\. Take \`train\_data\` (Input\[Dataset\]) as input.  
   2\. Train a Linear Regression model to predict 'sales' using 'tv', 'social', 'digital', and 'radio'.  
   3\. Save the trained model as an artifact \`model\` (Output\[Model\]).  
   4\. Use base image \`python:3.9\` and install \`pandas\` and \`scikit-learn\`.

2. **Review and Execute:** Click **Accept and Run** to define the training component.

### **Component 3: Evaluate Model**

1. Enter the prompt:  
   Plaintext  
   Write a third component named \`eval\_model\`.  
   It should:  
   1\. Take \`test\_data\` (Input\[Dataset\]) and the trained \`model\` (Input\[Model\]) as inputs.  
   2\. Predict sales on the test set.  
   3\. Calculate the Root Mean Squared Error (RMSE)  
   4\. Print the RMSE and log it as a pipeline metric.

2. **Review and Execute:** Click **Accept and Run** to define the evaluation component.

## **Task 4\. Orchestrate and Submit**

1. Now, ask the agent to wire it all together:  
   Plaintext  
   Create a pipeline definition function named \`media\_sales\_pipeline\` using \`@dsl.pipeline\`.  
   It should take \`url\` as an input argument.  
   Connect the three components: load \-\> train \-\> eval.  
   Then, write the code to compile and submit this pipeline run to Vertex AI.  
   Use this URL for the input: \`https://storage.googleapis.com/my-datasets-gs/media\_sales\_cymbal.csv\`  
   Set the pipeline\_root to \`gs://{{project\_id}}/pipeline\_root\`.

2. **Refine and Run:**  
   * Review the generated code. Ensure the load\_data component receives the URL correctly.  
   * Click **Accept and Run** to submit the pipeline.  
   * (Use **Cancel** if the agent missed a parameter, then re-prompt).  
3. **Monitor:**  
   * The output will generate a link to **Vertex AI Pipelines**.  
   * Click the link to watch your "Media Sales" pipeline execute. You will see the data flow from the GCS URL through the training step and finally output an accuracy metric.

## **Task 5\. Inspect Results**

1. Once the pipeline completes (all boxes green), click on the **eval\_model** component in the pipeline graph.  
2. Look at the **Artifacts** or **Metrics** tab in the side panel.  
3. You should see the **MAE** (Mean Absolute Error) value based on the Cymbal Media dataset.

## **Task 6\. Advanced: Go to Production**

Note: Here are the additional tasks to extend the lab. These steps guide the student to "chat" with the agent to iteratively upgrade their simple linear pipeline into a sophisticated, production-ready workflow.

Now that you have a working baseline pipeline, you will use the Data Science Agent to add "Production-Grade" features: **Hyperparameter Tuning**, **Conditional Deployment**, and **Model Registry Integration**.

### **Step 1: Internal Hyperparameter Tuning**

Instead of training a model with default settings, let's ask the Agent to upgrade our training component to automatically find the best parameters.

* In the Data Science Agent chat, enter the following prompt:  
  Plaintext  
  I need to improve the \`train\_model\` component.  
  Modify the code to use \`GridSearchCV\` from scikit-learn.  
  It should:  
  1\. Define a parameter grid for a RandomForestRegressor (e.g., trying different 'n\_estimators' and 'max\_depth').  
  2\. Perform cross-validation to find the best hyperparameters.  
  3\. Train the final model using the best parameters found.  
  4\. Save the best model as the artifact.

* **Review and Execute:**  
  * The Agent will generate a new version of the train\_model function.  
  * **Replace** your old train\_model cell with this new code and run it.

### **Step 2: Upload to Model Registry**

We don't just want a saved file; we want a registered model version that we can deploy to an endpoint.

6. Ask the Agent to create a new component for this:  
   Plaintext  
   Write a new pipeline component named \`upload\_model\`.  
   It should:  
   1\. Take the trained \`model\` (Input\[Model\]) as input.  
   2\. Use the \`google.cloud.aiplatform\` SDK to upload this model to the Vertex AI Model Registry.  
   3\. Give it the display name "media-sales-predictor".  
   4\. Use base image \`python:3.9\` and install \`google-cloud-aiplatform\`.

7. **Select Action:** Click **Accept and Run**.

### **Step 3: Conditional Deployment**

We only want to register the model if it's actually good. Let's add logic to check if the error (RMSE) is acceptable.

2. Ask the Agent to rewrite the pipeline definition to include the condition:  
   Plaintext  
   Rewrite the \`media\_sales\_pipeline\` function.  
   Add a conditional step using \`dsl.Condition\`.  
   Logic:  
   1\. Run \`load\_data\` and \`train\_model\` (the new GridSearchCV version).  
   2\. Run \`eval\_model\`.  
   3\. IF the RMSE output from \`eval\_model\` is less than 200 (choose a reasonable threshold):  
      \- Run the \`upload\_model\` component.  
   4\. ELSE:  
      \- Do not upload the model.

   *\> **Note:** You may need to update your eval\_model to output the RMSE as a simple output parameter (e.g., Output\[float\]) so the condition can read it easily. If the agent notices this dependency, let it update the evaluation component code too.*  
3. **Refine and Run:**  
   * Review the new pipeline graph code. Look for with dsl.Condition(...).  
   * **Execute the cell** to redefine the pipeline.  
   * **Submit** the pipeline run again.

### **Step 4: Verify the Advanced Pipeline**

2. Click the link to **Vertex AI Pipelines**.  
3. Watch the execution.  
   * **Scenario A (Good Model):** If your model is accurate (MAE \< 200), you will see the **upload\_model** step turn green. You can then go to the **Vertex AI Model Registry** page in the console to see your new "media-sales-predictor" model listed.  
   * **Scenario B (Bad Model):** If the model is poor, the condition will evaluate to false, and the upload step will be skipped (often shown as "Skipped" or greyed out).

## **Task 7\. Track and Compare with Vertex AI Experiments**

Note: Here are two additional tasks, **Task 7** and **Task 8**, that introduce **Vertex AI Experiments** for tracking model performance and **Pipeline Scheduling** for automation.

In the real world, you don't just train one model; you train dozens, tweaking parameters and algorithms to find the best one. Vertex AI Experiments lets you track these runs and compare metrics (like MAE) side-by-side. 

### **Step 1: Submit a Run as an Experiment**

Let's ask the Agent to submit our pipeline run specifically as an "Experiment" so we can track it.

* In the Data Science Agent chat, enter the following prompt:  
  Plaintext  
  I want to track my pipeline runs.  
  Write the Python code to submit my \`media\_sales\_pipeline\` as a Vertex AI Experiment.  
  1\. Name the experiment "media-sales-experiment".  
  2\. Name this specific run "run-random-forest-v1".  
  3\. Use the same pipeline root and parameters as before.

* **Select Action:** Click **Accept and Run**.  
* **Analyze:**  
  * The Agent will use the experiment parameter in the submit() or PipelineJob call.  
  * Once the run starts, go to the **Vertex AI** section in the Google Cloud Console.  
  * Click on **Experiments** in the left sidebar.  
  * Click **media-sales-experiment**. You will see your run listed there.

### **Step 2: Compare Runs (Optional)**

To see the power of experiments, you would ideally run the pipeline again with a different model (e.g., reverting to Linear Regression) and name it "run-linear-reg-v1". You would then see both runs in the Experiments table and could directly compare their MAE metrics to choose the winner.

## **Task 8\. Schedule the Pipeline**

Finally, a pipeline isn't useful if you have to manually click "Run" every time new data arrives. Let's automate this to run on a schedule.

8. Ask the Agent to schedule the pipeline:  
   Plaintext  
   I want this pipeline to run automatically.  
   Write the Python code to create a Schedule for this pipeline.  
   1\. It should run once every Monday at 9:00 AM.  
   2\. Use the display name "weekly-media-sales-retraining".  
   3\. Use the same pipeline definition and arguments.

9. **Select Action:** Click **Accept and Run**.  
10. **Verify:**  
    * The Agent will likely use aiplatform.PipelineJob.create\_schedule or the Schedule.create method.  
    * After running the code, navigate to **Vertex AI \> Schedules** in the Cloud Console.  
    * You should see your "weekly-media-sales-retraining" schedule listed and active\!

## **Congratulations\!**

Congratulations\! You have successfully orchestrated a complete, production-grade Machine Learning pipeline on Google Cloud.

In this lab, you used the **Data Science Agent** in Colab Enterprise to act as your expert pair programmer. You started by exploring a raw media sales dataset from Google Cloud Storage, then rapidly generated KFP components to ingest data, train a model, and evaluate its accuracy.

Going beyond the basics, you then iterated on your pipeline to add professional MLOps features. You implemented **hyperparameter tuning** to optimize your model's performance, added **conditional deployment logic** to ensure only high-quality models are saved, and integrated with the **Vertex AI Model Registry** for version control. Finally, you leveraged **Vertex AI Experiments** to track your run metrics and set up a **Pipeline Schedule** for fully automated weekly retraining.

You now have the skills to turn a manual modeling process into a robust, automated workflow using Vertex AI.

### **Next steps / learn more**

* [Vertex AI Pipelines Documentation](https://cloud.google.com/vertex-ai/docs/pipelines/introduction)  
* [Vertex AI Experiments](https://cloud.google.com/vertex-ai/docs/experiments/intro-vertex-ai-experiments)  
* [Vertex AI Model Registry](https://cloud.google.com/vertex-ai/docs/model-registry/introduction)

**Manual Last Updated December 24, 2025** **Lab Last Tested December 24, 2025**

Copyright 2025 Google LLC. All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.


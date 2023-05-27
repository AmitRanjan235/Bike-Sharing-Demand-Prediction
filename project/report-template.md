<!DOCTYPE html>
<html>
<head>
  <title>Report: Predict Bike Sharing Demand with AutoGluon Solution</title>
</head>
<body>
  <h1>Report: Predict Bike Sharing Demand with AutoGluon Solution</h1>
  <h3>Amit Ranjan</h3>

  <h2>Initial Training</h2>
  <h3>What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?</h3>
  <p>When I trained the model for the first time, it was trained on the default parameter settings without performing any EDA and feature engineering. The model's performance was severely lacking, with a validation RMSE score of 52.711828 and a Kaggle score of 1.80414.</p>
  <p>This indicates that the initial model was overfitted. To improve the model's performance, I added new features such as 'hour' and 'temp_humidity'. By incorporating these additional features, the accuracy of the model improved. The validation RMSE score for the 'add_features' model was 30.357975, and the Kaggle score was 0.65044. Although this model was still overfitted, it outperformed the initial model.</p>
  <p>Finally, to further address the overfitting issue, I performed hyperparameter optimization. By fine-tuning the model's parameters, I achieved a validation RMSE score of 34.824982 and the best Kaggle score of 0.46765 (on the test dataset).</p>

  <h3>What was the top-ranked model that performed?</h3>
  <p>The top-ranked model that performed was the 'hpo_model', which stands for hyperparameter optimized model. It utilized the WeightedEnsemble_L2 algorithm and achieved a validation RMSE score of 34.824982 and the best Kaggle score of 0.46765 (on the test dataset).</p>

  <h2>Exploratory data analysis and feature creation</h2>
  <h3>What did the exploratory analysis find and how did you add additional features?</h3>
  <p>Based on the exploratory analysis, the following findings were identified:</p>
  <ul>
    <li>Temperature (temp) and "Feels Like" Temperature (atemp) showed a high correlation, indicating their strong relationship. Both variables were also highly correlated with two other fields.</li>
    <li>Casual and registered users showed high correlations with temperature and other fields. Registered users were highly correlated with casual users and one other field.</li>
    <li>The total bike rentals (count) showed high correlations with casual users and one other field.</li>
    <li>Season exhibited a high correlation with temperature and one other field.</li>
    <li>The holiday variable was highly imbalanced, with 81.3% of records classified as non-holidays.</li>
    <li>Datetime had unique values, indicating a specific date and time for each observation.</li>
    <li>Windspeed had 1313 instances (12.1% of the dataset) with a value of zero, suggesting potential missing or inaccurate data.</li>
    <li>There were 986 instances (9.1% of the dataset) where the number of casual user rentals was zero.</li>
  </ul>
  <p>To address the insights gained from the exploratory analysis and leverage the correlations found among the variables, additional features were created:</p>
  <ul>
    <li>'Hour' feature: Extracted from the datetime variable using the dt.hour method, capturing the specific hour at which the bike rental occurred.</li>
    <li>'Hour Squared' feature: Computed the squared value of the hour feature to capture potential non-linear relationships associated with the hour variable.</li>
    <li>'Temperature and Humidity Interaction' feature: Created a new feature called 'temp_humidity' by multiplying the values of the temperature (temp) and humidity variables together, capturing the combined effect of temperature and humidity on bike rentals.</li>
  </ul>
  
  <h3>How much better did your model perform after adding additional features and why do you think that is?</h3>
  <p>The model's performance showed a significant improvement after adding the additional features. The initial model achieved a Kaggle score of 1.80414, while the 'add_features' model with the newly created features achieved a score of 0.65044. This improvement can be attributed to several factors:</p>
  <ul>
    <li>Enhanced Temporal Representation: The introduction of the 'hour' feature and its squared value allowed the model to capture non-linear temporal patterns that were not apparent before.</li>
    <li>Interaction between Variables: The 'temp_humidity' feature captured the combined impact of temperature and humidity on the target variable, enabling the model to better understand their joint influence.</li>
    <li>Improved Feature Space: The additional features expanded the feature space, providing the model with more diverse and informative input, leading to improved predictions.</li>
  </ul>
  <p>Overall, the addition of these features improved the model's performance by enhancing the temporal representation, capturing interactions between variables, and enriching the feature space.</p>

  <h2>Hyperparameter tuning</h2>
  <h3>How much better did your model perform after trying different hyperparameters?</h3>
  <p>The evaluation of model performance, measured by Kaggle scores, revealed notable improvements following the exploration of various hyperparameters:</p>
  <ul>
    <li>Initial Model: The initial model trained with default hyperparameter values achieved a Kaggle score of 1.80414.</li>
    <li>HPO Model: Through comprehensive hyperparameter optimization, the model's configuration was fine-tuned. The HPO Model exhibited a significant enhancement in performance, achieving a Kaggle score of 0.46765, indicating a substantial improvement in predictive accuracy.</li>
    <li>HPO1 Model: Further refinements were applied to the hyperparameters in the HPO1 Model. It showcased a slightly improved Kaggle score of 0.49301, indicating a modest yet noticeable enhancement in predictive performance.</li>
  </ul>
  <p>The observed improvements in model performance demonstrate the effectiveness of hyperparameter tuning in optimizing the model's performance and predictive accuracy.</p>

  <h3>If you were given more time with this dataset, where do you think you would spend more time?</h3>
  <p>If more time were available with this dataset, further areas for exploration and improvement could include:</p>
  <ul>
    <li>Feature engineering: Exploring and creating additional features based on domain knowledge or further analysis of the data.</li>
    <li>Model selection: Trying out different models or more advanced modeling techniques to find the best-performing algorithm for this specific dataset.</li>
    <li>Ensemble methods: Building ensemble models by combining multiple models to further enhance predictive performance.</li>
    <li>Advanced hyperparameter tuning: Employing more sophisticated hyperparameter optimization techniques such as Bayesian optimization or genetic algorithms to find even better hyperparameter configurations.</li>
    <li>Error analysis: Analyzing model errors, understanding the patterns of misclassifications or predictions, and refining the models based on these insights.</li>
  </ul>

  <h3>Create a table with the models you ran, the hyperparameters modified, and the Kaggle score.</h3>
  <table>
    <tr>
      <th>Model</th>
      <th>HPO1</th>
      <th>HPO2</th>
      <th>HPO3</th>
      <th>Score</th>
    </tr>
    <tr>
      <td>Initial Model</td>
      <td>Default values</td>
      <td>Default values</td>
      <td>Default values</td>
      <td>1.80414</td>
    </tr>
    <tr>
      <td>Add Features Model</td>
      <td>Default values</td>
      <td>Default values</td>
      <td>Default values</td>
      <td>0.65044</td>
    </tr>
    <tr>
      <td>HPO Model</td>
      <td>GBM: gbm_options</td>
      <td>RF: rf_options</td>
      <td>NN: nn_options</td>
      <td>0.46765</td>
    </tr>
    <tr>
      <td>HPO1 Model</td>
      <td>GBM</td>
      <td>RF</td>
      <td>XGB</td>
      <td>0.49301</td>
    </tr>
  </table>

  <h3>Create a line plot showing the top model score for the three (or more) training runs during the project.</h3>
  <img src="Udacity_aws_ai_ml/project/Bike-Sharing-Demand-Prediction/project/img/model_train_score.png" alt="Model Training Score">

  <h3>Create a line plot showing the top Kaggle score for the three (or more) prediction submissions during the project.</h3>
  <img src="Udacity_aws_ai_ml/project/Bike-Sharing-Demand-Prediction/project/img/model_test_score.png" alt="Model Test Score">

  <h2>Summary</h2>
  <p>Overall, through the iterative process of initial training, exploratory data analysis, feature creation, and hyperparameter tuning, the model's performance significantly improved. The addition of new features enhanced the model's understanding of temporal patterns and captured interactions between variables, leading to improved predictions. Hyperparameter tuning further optimized the model's performance, resulting in lower Kaggle scores. Given more time, additional improvements could be made through feature engineering, exploring different models or ensemble methods, and further hyperparameter optimization. The presented results highlight the importance of thorough analysis, feature engineering, and hyperparameter tuning in building successful predictive models.</p>
</body>
</html>

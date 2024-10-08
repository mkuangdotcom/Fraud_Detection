<h1>Fraudulent Transaction Detection Model</h1>

<h2>Purpose</h2>
<p>
    The rapid development in the financial industry has exposed significant risks, one of the most critical being the detection of fraudulent activities. This project aims to detect and predict fraudulent transactions by analyzing clients' transaction history, spending patterns, and account behaviors to identify anomalies and prevent financial losses.
</p>

<hr />

<h2>Dataset</h2>
<ul>
    <li><strong>Link</strong>: <a href="https://www.kaggle.com/datasets/sanskar457/fraud-transaction-detection/data">Fraud Transaction Detection Dataset</a></li>
    <li><strong>Description</strong>: 
        <ul>
            <li>The dataset contains 1.75 million transactions generated by simulated users over a period from January 2023 to June 2023.</li>
            <li>It is highly imbalanced, with only 0.1345% of transactions classified as fraudulent.</li>
        </ul>
    </li>
</ul>

<hr />

<h2>Project Overview</h2>

<h3>1. Data Analysis</h3>
<p><strong>Imbalance Issue</strong>: The dataset is imbalanced, meaning there are significantly fewer fraudulent transactions compared to legitimate ones. This imbalance could skew the model's performance.</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/93f7ee14-0d9d-49b8-8d6b-90a8a393fd77" />
</p>

<h3>2. Data Preprocessing</h3>
<p>To address the imbalance, we apply the <strong>Synthetic Minority Over-sampling Technique (SMOTE)</strong>. SMOTE helps generate synthetic samples for the minority class (fraudulent transactions), improving the model's ability to detect fraud.</p>
<p>Before applying SMOTE, the data is split to ensure that the validation dataset remains untouched, allowing the model to be evaluated on real, unaltered data.</p>

<h4>Steps:</h4>
<ol>
    <li><strong>Train-Test Split</strong>:
        <p>The dataset is divided into training and testing sets using an 80/20 ratio. We apply <strong>SMOTE</strong> to the training set only to balance the class distribution. The test set remains imbalanced, allowing for unbiased evaluation of model performance on real-world data.</p>
    </li>
    <li><strong>Preprocessing</strong>:
        <ul>
            <li><strong>Min-Max Scaling</strong>: All numeric features (e.g., transaction amount) are scaled between 0 and 1 using <code>MinMaxScaler()</code>, ensuring that features with larger ranges don’t dominate the model training process.</li>
            <li><strong>Categorical Encoding</strong>: Categorical features (e.g., customer ID, terminal ID) are encoded using <code>OneHotEncoder(handle_unknown='ignore')</code>, which creates binary columns for each category to help the model understand categorical variables.</li>
        </ul>
    </li>
</ol>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3fa8e454-2633-431d-b1fd-f5cb657fd935" />
</p>

<hr />

<h3>3. Model Development</h3>
<p>We employ a <strong>Keras Sequential Neural Network</strong> to classify transactions as fraudulent or legitimate. Here’s the model architecture:</p>

<pre>
<code>
nn_model = keras.Sequential([
    keras.layers.Input(shape=(X_train_resampled.shape[1],)),
    keras.layers.Dense(64, activation='relu'),
    keras.layers.Dropout(0.2), 
    keras.layers.Dense(32, activation='relu'),
    keras.layers.Dropout(0.2), 
    keras.layers.Dense(1, activation='sigmoid')
])
</code>
</pre>

<p><strong>Dropout Layers</strong>: Dropout layers help in reducing overfitting, especially in highly imbalanced datasets, by randomly turning off a fraction of neurons during training. This forces the model to learn more robust patterns.</p>

<hr />

<h3>4. Results</h3>

<h4>Training History</h4>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3d574226-7b1a-4171-8c87-3c92e2000081" />
</p>

<p>The training and validation accuracy do not show significant divergence or fluctuations, indicating the model is performing well despite the class imbalance.</p>

<h4 style="text-align: center;">Confusion Matrix</h4>
<p align="center">
  <img src="https://github.com/user-attachments/assets/6986c0cb-7382-4133-bd1f-9b8b773ce0fb" />
</p>

<h4>Classification Report</h4>

<table border="1">
    <thead>
        <tr>
            <th>Metric</th>
            <th>Precision</th>
            <th>Recall</th>
            <th>F1-Score</th>
            <th>Support</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Legitimate Transactions (0)</strong></td>
            <td>0.96</td>
            <td>0.96</td>
            <td>0.96</td>
            <td>303,637</td>
        </tr>
        <tr>
            <td><strong>Fraudulent Transactions (1)</strong></td>
            <td>0.74</td>
            <td>0.73</td>
            <td>0.74</td>
            <td>47,194</td>
        </tr>
        <tr>
            <td><strong>Accuracy</strong></td>
            <td colspan="4"><strong>0.93</strong></td>
        </tr>
        <tr>
            <td><strong>Macro Avg</strong></td>
            <td>0.85</td>
            <td>0.85</td>
            <td>0.85</td>
            <td>350,831</td>
        </tr>
        <tr>
            <td><strong>Weighted Avg</strong></td>
            <td>0.93</td>
            <td>0.93</td>
            <td>0.93</td>
            <td>350,831</td>
        </tr>
    </tbody>
</table>

<hr />

<h2>Conclusion</h2>
<p>
    The model achieved an accuracy of 93%, with a precision and recall of 0.74 for detecting fraudulent transactions. 
    The results suggest that the model can identify fraudulent activity effectively, but there’s room for improvement, 
    especially in the recall for fraudulent transactions. Fine-tuning the model, trying alternative algorithms, and 
    leveraging more advanced techniques like ensemble learning could further improve the performance.
</p>

</body>
</html>

# Vehicle-Trajectory-Management
This project implements a vehicle trajectory prediction model based on attention mechanisms and inverse reinforcement learning (IRL). The aim is to accurately predict vehicle trajectories by learning from real-world driving data and focusing on key environmental factors using attention-based neural networks.


## Dataset
The dataset required for this project is available [here](https://drive.google.com/drive/folders/1wlT7E1dJ4I-D-7t0fN5DhWLt5uLT9eUi) on Google Drive. It contains real-world vehicle trajectory data collected in various traffic conditions.


## Cell-by-Cell Explanation
### Cell 1: Import Libraries
This cell imports essential libraries required for data handling, visualization, and machine learning.
  - `pandas`, `numpy`: Used for data manipulation and numerical operations.
  - `matplotlib.pyplot`, `seaborn`: Utilized for data visualization.
  - `sklearn`: A popular machine learning library for model training and evaluation.
  - `tensorflow` or `keras`: Likely used for building neural network models if trajectory prediction involves deep learning.

### Cell 2: Load Data
This cell loads the dataset, `vehicle_data.csv`, which seems to contain information on vehicle trajectories.
  - `pd.read_csv()`: Reads the CSV file and loads it into a Pandas DataFrame, making it easy to explore and manipulate.
  - `head()`: Displays the first few rows to get a sense of the data structure, such as columns and initial values.

### Cell 3: Data Exploration and Preprocessing
This cell examines the data for any issues that may need preprocessing before modeling.
  - `info()`: Shows the column types and helps identify any missing values or data types that may require adjustments.
  - `describe()`: Provides summary statistics for numerical columns, giving insights into the distribution and range of values, which could influence scaling or normalization steps.

### Cell 4: Feature Selection and Engineering
Feature selection and engineering are crucial steps in any machine learning project, especially for tasks like vehicle trajectory prediction, which can depend on time series and spatial data. Here’s a detailed breakdown of what might be done in this cell:
  -  **Purpose of Data Splitting**
    
     This step involves selecting columns that contain information directly useful for predicting vehicle trajectories. In a trajectory dataset, common features might include:
      - **Timestamp**: Indicates the time associated with each observation. Time series data is critical for trajectory prediction as it allows the model to understand movement over time.
      - **Location (Latitude, Longitude)**: Coordinates that show the vehicle's position. Sometimes, Cartesian coordinates (X, Y) are derived from latitude and longitude for easier       
        computation.
      - **Speed**: The velocity of the vehicle at each timestamp, which can help infer movement patterns.
      - **Heading**: The direction the vehicle is facing, which helps predict its future path.
   
        
  -  **Feature Engineering**
    
     In feature engineering, you create additional useful features from existing ones, or you transform data to make it more suitable for modeling.
      - **Velocity Components**: Break down speed into x and y components based on the heading angle to represent directional movement.
      - **Acceleration**: Calculate the change in speed over time to provide insights into how the vehicle’s motion is changing.
      - **Displacement Vectors**: Define vectors that capture changes in location between successive timestamps, giving the model more dynamic spatial information.
      - **Time-Based Features**: For time-series predictions, deriving features like the time of day, day of the week, or even calculating time differences between records can improve model performance.
   



  - **Normalization or Standardization**
    
    Since neural networks (if being used) work better with normalized or standardized data, it’s often essential to scale features, especially those with large or uneven ranges (e.g., latitude/longitude vs. speed).

    - **Min-Max Scaling**: Often used for positional and directional data to bring values into a [0, 1] range.
    - **Standard Scaling**: Makes features have a mean of 0 and standard deviation of 1, which is common for speed and acceleration.
- **Encoding Categorical Features**

    If the dataset contains categorical data, such as the vehicle type (e.g., car, truck, motorcycle), it may be encoded as numerical data using one-hot encoding or label encoding.

### Cell 5: Splitting Data into Train and Test Sets

Splitting data is essential for evaluating model performance effectively by ensuring that training and testing occur on separate subsets of the data.

- **Purpose of Data Splitting**: 

    Dividing the dataset into training and testing sets ensures that the model learns patterns only from the training data and is evaluated on unseen data to measure its generalization ability. This setup mimics real-world scenarios, where models must make predictions on new data.

- **`train_test_split()` Function**

    The `train_test_split()` function from `sklearn.model_selection` is commonly used for this step. This function:

    - **Randomly splits the data** based on a specified test_size parameter, usually set around 0.2 or 0.3 (indicating that 20-30% of data is for testing).
    - **Stratifies the split** (if applicable) to maintain proportional representation of categories within the training and test sets.


- **Resulting Train and Test Sets**

    After splitting, you get four variables:

    - **`X_train`, `X_test`**: Feature sets for training and testing.
    - **`y_train`, `y_test`**: Target labels (i.e., the vehicle’s future position or trajectory) for training and testing.


## RSME per Batch on Test Dataset
<p align="center">
  <img src="Screenshot from 2024-11-12 10-01-55[1].png" width="300" height="300" />
</p>

## Ground V/S Predicted Trajectory
<p align="center">
  <img src="Screenshot from 2024-11-12 10-31-15.png" width="300" height="300" />
</p>

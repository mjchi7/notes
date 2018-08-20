# notes
Tips/Tricks/Notes encountered during development

# Pandas
## 1. Explicit logical operator needed
- do not use "not", "is" when comparing pd.DataFrame or pd.Series's cell value.
- Explicitly put parantheses around a boolean returning operation. eg.:
    ``` python
    #NO: 
    df['A'] == 'aa' & df['B'] == 'cc'
    #YES: 
    (df['A'] == 'aa') & (df['B'] == 'cc')
    ```
## 2. JSON cannot serialize numpy type
- When trying to serialize numpy's type (np.int64, np.float64,..), error will be thrown complaining:
  
## 3. Matplotlib backend
### 3.1 Mac OSX Matplotlib backend
- Download pyqt5 and pyside2
- Right after import statement, make matplotlib use Qt5Agg backend
    ``` python
    import matplotlib
    matplotlib.use('Qt5Agg')
    import matplotlib.pyplot as plt
    ```
### 3.2 Linux CentOS Matplotlib backend
- Use 'agg' backend for Linux CentOS
    ``` python
    import matplotlib
    matplotlib.use('agg')
    import matplotlib.pyplot as plt
    ```

## 4.XGBoost 
### 4.1 xgboost.XGBRegressor.fit() v.s. xgboost.train()
- Both are actually doing the same thing (fitting training data to training label). However, in the parameter list, xgboost.XGBRegressor takes in n_estimators, while xgboost.train() takes num_boost_rounds 
- Reference: https://stackoverflow.com/questions/46943674/how-to-get-predictions-with-xgboost-and-xgboost-using-scikit-learn-wrapper-to-ma

## 5. Gradient Boosted Trees Visualization
- Great details on how gradient boosted trees work in code terms. 
- Understanding how tree is constructed is a challenge though.
- https://www.kaggle.com/grroverpr/gradient-boosting-simplified/

## 6. Pandas Dataframe
### 6.1 Accessing underlying np.array with .values
- To manipulate the dataframe's underlying np.array, use column.value
- For example:
    ``` python
    idx_ = df.index.values
    col1_ = df.col1.values
    col2_ = df.col2.values
   ```
- Any manipulation done on the ".values" will be reflected in the dataframe. 
- For example:
    ``` python
    col1_[10] = 8 
    # then
    print(df.loc[10, 'col1'])
    -> 8
    ```
### 6.2 Performance improvement
- Using my current setup, manipulating dataframe directly takes 0.2 seconds for the following operation
    ``` python
    df.loc[idx, 'gen_make'] = df.loc[idx, 'gen_model'].replace("series", "") + substring
    ```
- If the same operation is performed on underlying np.array, it takes 7.3e-6 seconds. Improvement up to 25,000!
    ``` python
    make_ = df.gen_make.values # To get the pointer for "gen_make" column in dataframe df
    # SAME OPERATION AS BEFORE
    make_[idx] = make[idx].replace("series","") + substring
    ```

   

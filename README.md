# notes
Tips/Tricks/Notes encountered during development

# Pandas
## 1. Explicit logical operator needed
- do not use "not", "is" when comparing pd.DataFrame or pd.Series's cell value.
- Explicitly put parantheses around a boolean returning operation. eg.:
    ``` python
    NO: 
    df['A'] == 'aa' & df['B'] == 'cc'
    YES: 
    (df['A'] == 'aa') & (df['B'] == 'cc')
    ```
## 2. JSON cannot serialize numpy type
- When trying to serialize numpy's type (np.int64, np.float64,..), error will be thrown complaining:
  "

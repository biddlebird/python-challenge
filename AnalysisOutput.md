### Analysis of the PyBank and PyPoll Coding Projects

This project involves analyzing financial data and election data using Python's Pandas library. Below is a breakdown and analysis of each part of the project:

---

### PyBank Analysis

#### Code Overview:
1. **Loading Data:**
   ```python
   import pandas as pd
   csv_path = '/Users/kaylabiddle/Downloads/Starter_Code-3/PyBank/Resources/budget_data.csv'
   budget_data = pd.read_csv(csv_path)
   budget_data.head()
   ```
   This code snippet loads a CSV file containing monthly financial data into a Pandas DataFrame and displays the first few rows.

2. **Total Number of Months:**
   ```python
   def calculate_total_months(df):
       total_months = df["Date"].nunique()
       return total_months
   ```
   This function calculates the total number of unique months in the dataset, providing an overview of the time period covered.

3. **Net Total of Profit/Losses:**
   ```python
   def calculate_total_profit(df):
       profit = df["Profit/Losses"].sum()
       return profit
   ```
   Computes the net total profit or loss by summing the values in the `Profit/Losses` column.

4. **Average Monthly Change:**
   ```python
   def calculate_average_change(df):
       df['Monthly Change'] = df["Profit/Losses"].diff()
       average_change = df['Monthly Change'][1:].mean()
       return average_change
   ```
   Calculates the average change in profit/losses from month to month by using the `diff()` method to find monthly differences and then averaging these values.

5. **Greatest Increase and Decrease in Profits:**
   ```python
   def calculate_greatest_increase(df):
       max_increase = df['Monthly Change'].max()
       max_increase_date = df.loc[df['Monthly Change'] == max_increase, 'Date'].iloc[0]
       return max_increase_date, max_increase

   def calculate_greatest_decrease(df):
       max_decrease = df['Monthly Change'].min()
       max_decrease_date = df.loc[df['Monthly Change'] == max_decrease, 'Date'].iloc[0]
       return max_decrease_date, max_decrease
   ```
   Identifies the largest increase and decrease in monthly profits, along with their respective dates.

6. **Printing Results:**
   ```python
   print(f"Total number of months: {total_months}")
   print(f"Total: ${total_profit}")
   print(f"Average Change: ${average_change:.2f}")
   print(f"Greatest Increase in Profits: {greatest_increase_date} (${greatest_increase})")
   print(f"Greatest Decrease in Profits: {greatest_decrease_date} (${greatest_decrease})")
   ```
   Outputs the calculated financial metrics, summarizing the overall financial performance.

**Summary of Results:**

- **Total Number of Months:** 86
- **Total Profit/Losses:** $22,564,198
- **Average Monthly Change:** -$8,311.11
- **Greatest Increase in Profits:** Aug-16 ($1,862,002)
- **Greatest Decrease in Profits:** Feb-14 ($-1,825,558)

---

### PyPoll Analysis

#### Code Overview:
1. **Loading Data:**
   ```python
   import pandas as pd
   from collections import Counter
   csv_path = '/Users/kaylabiddle/Downloads/Starter_Code-3/PyPoll/Resources/election_data.csv'
   voting_data = pd.read_csv(csv_path)
   voting_data.head()
   ```
   This code snippet loads a CSV file containing election data into a Pandas DataFrame and displays the first few rows.

2. **Total Number of Votes Cast:**
   ```python
   def calculate_total_votes(df):
       total_votes = df["Ballot ID"].nunique()
       return total_votes
   ```
   Calculates the total number of unique votes cast by counting the unique entries in the `Ballot ID` column.

3. **List of Candidates and Their Vote Percentages:**
   ```python
   def calculate_candidate_list(df):
       names = df["Candidate"]
       name_counts = Counter(names)
       return name_counts

   name_counts = calculate_candidate_list(voting_data)
   for name, count in name_counts.items():
       percentage = (count / total_votes) * 100
       print(f"•{name}: {percentage:.3f}% ({count})")
   ```
   Generates a list of candidates, their total votes, and the percentage of votes each candidate received. Uses the `Counter` class to count votes and calculates percentages.

4. **Determining the Winner:**
   ```python
   def calculate_winner(df):
       names = df["Candidate"]
       name_counts = Counter(names)
       most_votes = name_counts.most_common(1)[0]
       return most_votes

   most_votes = calculate_winner(voting_data)
   winner_name = most_votes[0]
   print(f"Winner: {winner_name}")
   ```
   Identifies the candidate with the highest number of votes and declares them as the winner.

**Summary of Results:**

- **Total Votes Cast:** 369,711
- **Charles Casper Stockham:** 23.049% (85,213 votes)
- **Diana DeGette:** 73.812% (272,892 votes)
- **Raymon Anthony Doane:** 3.139% (11,606 votes)
- **Winner:** Diana DeGette

---

### Conclusion

This project demonstrates practical applications of data analysis using Pandas. The PyBank analysis provides insights into financial trends, including total profits, average changes, and significant fluctuations. The PyPoll analysis offers a detailed breakdown of election results, including the total votes, candidate performance, and the election winner. Together, these analyses showcase the power of Python for handling and interpreting data in real-world scenarios.

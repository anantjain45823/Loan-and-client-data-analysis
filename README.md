# Loan-and-client-data-analysis
This repo contains analysis of loan and client data
Requirements.txt -> all opython libraries which need to be installed 
problems.txt -> problems faced for doing some particular operations
clients.csv and loans.csv -> CSV files to perform analysis on

Steps Performed:
  1. Installing and Importing Libraries
  2. Reading Data from CSV 
  3. Connecting to Postgres DB
  4. Data Analysis -> For all the CSV provided doing some elemenatry data viz and checking data quality
  5. Case Resolutions
     a. Database -> Storing CSV in DB and explaining relationship between them
     b. SQl and Data Viz. -> Playing with and Visualing data to fetch some answers from SQL tables
     c. Python and infra -> constructing email reminders for loans based upon due_date, generating functions schema for ensuring operations run smoothly

Summary for Analysis :
1. To get the best 10 users I used the following method
      # basic conditions would be (after normalising all the metrics)
            # user_denied = 0 i.e. user status is not denied
            # loan_default_rate = 0.0 i.e. no loans resulted in default
            # loan_paid_to_total_loan > 0.7 i.e. more than 70% of loan amount is paid currently
            # actual_profit_till_date > 0.3 i.e. ensures profit should be greater than 30% clients
      # Applying weights 
         `average_loan_repayment_time` is inversely proportional to customer quality. hence weight => -1 
         `loan_repaid_to_total_loan`, `actual_profit_till_date` is directly proportional to customer quality
3. To get the worst 10 users I used the following method
      # basic conditions would be (after normalising all the metrics)
        # user_denied = 1 i.e. user status is  denied
        # loan_default_rate > 0.5 i.e. more than 50 % loans resulted in default
        # loan_paid_to_total_loan < 0.7 i.e. less than 70% of loan amount is paid currently
        # loan_amount_left > 0.3 i.e. ensures amount should be greater than 30% clients
     # Applying weights 
        # `loan_default_rate`, `average_loan_repayment_time` is inversely proportional to customer quality. hence weight => -1 
        # `loan_repaid_to_total_loan`, `actual_profit_till_date` is directly proportional to customer quality
5. To get batch adherence
     # Applying Weights
        # more denial_rate, loan_default_rate, amount_under_default_to_total_left_amount, average_loan_repayment_time less better batch hence weighting it with -1
        # Rest are directly proportional to how better a batch is hence multiplying with +1 weight

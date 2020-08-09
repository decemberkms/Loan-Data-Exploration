# Loan Data Exploration

## Dataset

This data set (`prosperLoanData.csv`) has 113937  rows and 81 columns (`BorrowerRate, Occupation, Borrower State.. etc`).
borrower rate (or interest rate), current loan status, borrower income, and many others.
The project objective is not expected to explore all of the variables in the dataset! But focus on only exploration on about 10-15 of them.

## Insights of the research

In this research, I focused on the features that determine interest rate `BorrowerRate`
I started with looking at the distrbuiton of some numeric and categorical variables that are expected to be meaningful for `BorrowerRate` and carried out bivariate and mulitvariate analysis in order to figure out relationships between `BorrowerRate` and the other variables. 

The major insights are :

#### Univariate Exploration
##### Categorical (Qualitative)
- Term int64 -> category: Most of the loans have 36 months and less than 2 %of the borrowers have 12 month loans.
- ProsperRating (Alpha) category: ProsperRating shows a symmetric  distribution. The main group of the borrowers have C and only few people have AA grade.
- CreditGrade category: Unlike ProsperRate, CreditGrade shows more AA grades than A grades. Furthermore, HR group is more than E and A groups.
- ProsperScore category: Most of the borrowers have between 4 to 8 ProsperScore.  
- ListingCategory category: The main purpose of loan is `Debt Consolidation` and we can see `Not Available` and `Other` in the second and third places respectively. The next common purpose is `Home Improvement` and `Business`.
- Occupation object: The borrowers are mostly `Professional` and `Sales` people (except for `Other` at the top)
- EmploymentStatus object: The majority of the borrowers is employed (categorised as Employed or Full-time). Interestingly, there is even retired people.
- IsBorrowerHomeowner bool: In terms of whether the borrowers are homeowner or not, the ratio is half and half.
- IncomeRange category,  IncomeVerifiable bool: As for `IncomeRange`, the main groups are \\$50,000-74,999 and \\$25,000-49,999 and there are more people of IncomeRange over \\$75,000 than below \\$24,999 or no income. Regarding IncomeVerifiable, more than 90% incomes are verifiable although there are around 8% incomes which are not verifiable.

##### Quantitative
- EmploymentStatusDuration float64: The majoriy of `EmploymentStatusDuration` is 0 ~ 200 months. Furthermore,since the natural histogram of `EmploymentStatusDuration` is skewed to the right, I changed the value into log scale. 
- StatedMonthlyIncome float64: The natural plot of `StatedMonthlyIncome`is skewed strongly to the right. So I first changed the plot to logscale then set the limit between 1.5 to 5.5.  Most of the borrowers get monthly less than \\$10,000. 
- MonthlyLoanPayment float64: In terms of `MonthlyLoanPayment`, we can see four peaks on the plot, at \\$190, at \\$320 , at \\$500 at \\$830. 
- LoanOriginalAmount int64: There is a pattern in the char of `LoanOriginalAmount`. Many loans are the amount of multiples of 5,000 (5000, 10000, 15000, 20000.. etc)
- DebtToIncomeRatio int64: The borrowers mainly have `DebtToIncomeRatio` less than 1 but there are around 800 people with `DebtToIncomeRatio` over 1

#### Bivariate Exploration
##### Relationship between `BorrowerRate` and  other `quantitative variables`
##### correlation plot
- `MonthlyLoanPayment` and `LoanOriginalAmount` show a strong positive correlation among the quantitative variables (not with `BorrowerRate`). However, there are not any positive correlations between `BorrowerRate` and the other quantitative variables, while `LoanOriginalAmount` and `MonthlyLoanPayment` show weak negative correlations (-0.33, -0.25 respectively) with `BorrowerRate`.

##### Relationship between `BorrowerRate` and  other `categorical variables`
##### BorrowerRate with ProsperRating (Alpha), CreditGrade, and ProsperScore
- It is clear that the better `CreditGrade/ProsperRating (Alpha)/ProsperScore` (three scores related to credit) is, the lower `BorrowerRate` is. 

##### BorrowerRate by EmploymentStatus, IncomeRange
- When it comes to `EmploymentStatus` and `IncomeRange`, `EmploymentStatus` shows that emplpoyed borrowers (`Full-time` and `Employed`) have the lowest `BorrowerRate`, while `Not Employed` has the highest interest rate. Besides, it is clear that the higher the person's income is, the lower interest he/she gets according to the `IncomeRage vs. BorrowerRate` box plot down to \\$0 income. Interestingly, \\$0 income people have lower `BorrowerRate` than \\$50,000-\\$74,999, \\$25,000-\\$49,999, and \\$1-\\$24,999. However, if they're not employed (`Not employed`) you get the highest interest rate like in `EmploymentStatus vs. BorrowerRate` plot.
##### BorrowerRate with IsBorrowerHomeowner and IncomeVerifiable
- The borrowers having houses also get lower `BorrowerRate` than the others. Morevoer, if the borrowers verify their income, they get lower interest rate. 


#### Multivariate Exploration
##### What is the relationship between BorrowerRate and IncomeRange by ProsperRating (Alpha), ProsperScore, CreditGrade?
- There is neither high positive nor negative correlations between borrowers' incomes and the interest rate. Instead, `BorrowerRating` shows a rather constant relationship with borrowers' `ProsperRating (Alpha)`, `ProsperScore`, `CreditGrade`. Even if a person has a low income, if the person has a high credit score or rating, the interest rate is the same as a persion with a high income and high grade.

##### What if put both IncomeVerifiable and IsBorrowerHomeowner together?
- There are no conspicuous relationships between `BorrowerRate` and `IncomeVerifiable`, `IsBorrowerHomeowner`.

##### Deep look into the relationship between BorrowerRate vs. rosperRating (Alpha) by IsBorrowerHomeowner and IncomeVerifiable.
- While the trend that the better the credit rating/score, the lower the interest rate exsist, there is a slight difference in `BorrowerRate` depending on `IncomeVerifiable` and `IsBorrowerHomeowner`. Nonetheless, the difference is less than 0.1 % at each `ProsperRating (Alpha)`. 


In conclusion, according to our analysis conducted so far, it is clear that interest rate (`BorrowerRate`) is highly dependant on `CreditGrade`, `ProsperRating (Alpha)`, and `ProsperScore`. Other variables like `IncomeRange`,`IncomeVerifiable` or `IsBorrowerHomeowner` also play a role in determining interest rate but it is minor comapred to `CreditGrade`, `ProsperRating (Alpha)`, and `ProsperScore`. Especially, I expected that `IncomeRange` would play a major role for `BorrowerRate` at the beginnning of this research, but in fact, it is not a essential factor for determining interest rate according to our research. Instead, regardless of a borrower's income, if the person has a good credit rating or score (`CreditGrade`, `ProsperRating (Alpha)`, or `ProsperScore`) then the person can get a low interest rate.
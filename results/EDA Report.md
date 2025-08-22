# EDA Report on Bank Marking Dataset

## Step 1: Dataset Loading
- ### Dataset: https://www.kaggle.com/datasets/janiobachmann/bank-marketing-dataset/data
- ### Original Source:  [Moro et al., 2014] S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014
- ### Tool: Python, Pandas, Numpy, Matplotlib, Seaborn, Scipy
##
## Step 2: Data Profiliing and Quality Check
### Step 2-1: Dataset Overview
- #### Detailed Column Description: See [bank_description](bank_description.md)
- #### Schema and Data Types
    - #### Number of columns: 17
    - #### Number of records: 11162
    - #### Data Types: int64, object
- #### Class Distribution
    - #### Distinct Class Value: Yes, No
    - #### Distribution: Yes (5289) - 47%, No (5873) - 53%
    - #### Relatively balanced class
- #### Missing Value Analysis
    - ##### No missing data is found
##
### Step 2-2: Inspect Numerical Type Columns for Distribution
<table>
  <thead>
    <tr>
      <th style="text-align: center;">Column Name</th>
      <th style="text-align: center;">Central Tendency</th>
      <th style="text-align: center;">Dispersion & Distribution Shape</th>
      <th style="text-align: center;">Outlier</th>
      <th style="text-align: center;">Regulatory & Operation Flag</th>
      <th style="text-align: center;">Feature Engineering</th>
    </tr>
  </thead>
  <tbody>
    <tr style="text-align: center;">
      <td>Age</td>
      <td style="text-align: left;">
        <ul>
            <li>Mean(41.23), Median(39), Mode(31): not equal -> non-normal distribution
            <li>Mean > Median > Mode: Positively skewed (right-skewed)
            <li>Mean > Median: could have outliers
            <li>Mode = 31: most of data come from younger population
        </ul>
      </td>
      <td style="text-align: left;">
        <ul>
            <li>CV=0.29: Moderate spread.
            <li>IQR << Median: Middle 50% data is tightly clustered around median.
            <li>Max > Q3 + 1.5 * IQR: Outlier presence.
            <li>Skew is 0.86: Moderate right-skewed.
            <li>Kurtosis > 0: Sharper peak and heavier tail.
        </ul>
      </td>
      <td>171 Presence (1.53%) by IQR</td>
      <td>Max = 95: need to check if this is valid per regulation</td>
      <td>Binning (by quantile) might be helpful if models didn't perform well on raw data.</td>
    </tr>
    <tr style="text-align: center;">
      <td>Balance</td>
      <td style="text-align: left;">
        <ul>
            <li>Mean(1528), Median(550), Mode(0): not equal -> non-normal distribution
            <li>Mean >> Median >> Mode: Positively skewed (right-skewed)
            <li>Mean >> Median: Outlier presence
            <li>Mode = 0: most people's average yearly balance is 0
        </ul>
      </td>
      <td style="text-align: left;">
        <ul>
            <li>CV=2.11: High degree of spread.
            <li>IQR >> Median: Spread of middle 50% data is wider than the bottom 50% (right-skewed).
            <li>Min < Q1 - 1.5 * IQR & Max > Q3 + 1.5 * IQR: Outlier presence.
            <li>Skew is 8.22: Extreme right-skewed.
            <li>Kurtosis is 126.8: Extremely sharp peak and heavy tail.
        </ul>
      </td>
      <td>1055 Presence (9.45%) by IQR</td>
      <td>Min = -6847: need to check if this is valid per regulation or potentially high risk candidate</td>
      <td>Consider logarithm transform to mitigate skewness</td>
    </tr>
    <tr style="text-align: center;">
      <td>Date</td>
      <td style="text-align: left;">
        <ul>
            <li>Mean(15.6), Median(15), Mode(20): Symmetric distribution.
        </ul>
      </td>
      <td style="text-align: left;">
        <ul>
            <li>CV=0.54: Moderate degree of spread.
            <li>IQR ~ Median: Spread of middle 50% data is similar to the bottom 50%.
            <li>Per IQR, no outlier presence. Combined with above metrics, the distribuion might be uniform across the range. (Still with other possibility)
            <li>Skew is 0.11: Fairly symmetrical.
            <li>Kurtosis is -1.06: Flatter peak and thinner tails.
        </ul>
      </td>
      <td>No Presence by IQR</td>
      <td>Per distribution visualization, it is multi-modal. It could imply the responsiveness due to paycheck schedule, call-center operation, marketing strategy etc.</td>
      <td>Cyclic encoding</td>
    </tr>
    <tr style="text-align: center;">
      <td>Duration</td>
      <td style="text-align: left;">
        <ul>
            <li>Mean(372) > Median(255) >> Mode(97): Right-skewed distribution.
        </ul>
      </td>
      <td style="text-align: left;">
        <ul>
            <li>CV=0.93: Moderate to high degree of spread.
            <li>IQR (358) > Median (255): Spread of middle 50% data is larger than the bottom 50%.
            <li>Max > 1.5 * IQR: Outlier presence.
            <li>Skew is 2.14: Right-skewed.
            <li>Kurtosis is 7.3: High peak and heavier tail.
        </ul>
      </td>
      <td>636 Presence (5.7%) by IQR</td>
      <td>Min is 2 may indicate a no-contact event.</td>
      <td style="text-align: left;">
        <ul>
            <li>New column for no-contact flag
            <li>Logarithm for outlier mitigation
        </ul>
      </td>
    </tr>
    <tr style="text-align: center;">
      <td>Campaign</td>
      <td style="text-align: left;">
        <ul>
            <li>Mean(2.51) > Median(2) > Mode(1): Right-skewed distribution.
        </ul>
      </td>
      <td style="text-align: left;">
        <ul>
            <li>CV=1.09: high degree of spread.
            <li>IQR (2) = Median: could be symmetric or highly clustered around median
            <li>Max > 1.5 * IQR: Outlier presence.
            <li>Skew is 5.54: Highly right-skewed.
            <li>Kurtosis is 57.36: Extremely high peak and heavier tail.
        </ul>
      </td>
      <td>601 Presence (5.38%) by IQR</td>
      <td>Max is 63: indicate extremely high contacts</td>
      <td style="text-align: left;">
        <ul>
            <li>New column for campaign * duration from semantic perspective
            <li>Binning or logarithm transformation
        </ul>
      </td>
    </tr>
    <tr style="text-align: center;">
      <td>Pdays</td>
      <td style="text-align: left;" colspan=5>
        The day after last contact should be non-zero but majority of pdays is -1.<br/>
        This column should be discarded as problematic values.
      </td>
    </tr>
    <tr style="text-align: center;">
      <td>Previous</td>
      <td style="text-align: left;">
        <ul>
            <li>Mean(0.83) > Median(0) = Mode(0): Right-skewed distribution.
        </ul>
      </td>
      <td style="text-align: left;">
        <ul>
            <li>CV=2.75: high degree of spread.
            <li>IQR (1) > Median: Right-skewed
            <li>Max > 1.5 * IQR: Outlier presence.
            <li>Skew is 7.33: Highly right-skewed.
            <li>Kurtosis is 106.15: Extremely high peak and heavier tail.
        </ul>
      </td>
      <td>1258 Presence (11.27%) by IQR</td>
      <td>Max is 58: indicate extremely high contacts</td>
      <td style="text-align: left;">
        <ul>
            <li>New column for campaign * duration from semantic perspective
            <li>Binning or logarithm transformation
        </ul>
      </td>
    </tr>
  </tbody>
</table>
 
### Step 2-3: Inspect Categorical Type Columns for Distinct Values
|Categorical Column|High Cardinality|Dominant Category|Meaningless Value|Temporal Drift|Encoding Inconsistency|Semantic Redundancy|Feature Engineering|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Job|No, 12 distinct values|No, most one accounts for 23%|'Unknown': 0.63%|Not found|Not found|Not found|- One-hot encoding<br>Per biz frame, could consider group some, e.g. management & entrepreneur or group rare jobs into 'other'
|Marital|No, 3 distinct values|Yes, 'married': 56.9%<br>Could be key differentiator|Not found|Not found|Not found|Not found|- One-hot encoding<br>- Binary grouping because 'single' has higher target association.|
|Education|No, 4 distinct values|Yes, 'secondary': 49%<br>Could be key differentiator|Yes, 'unknown':4.45%|Not found|Not found|Not found|- One-hot encoding<br>- Ordinal mapping: unknown < primary < secondary < tertiary|
|Contact|No, 3 distinct values|Yes, 'Cellular': 72%|'Unknown': 21%|Not found|Not found|Not found|- One-hot encoding
|Month|No, 12 distinct values|No, most one accounts for 25%|Not found|Not found|Not found|Not found|- Cyclic encoding<br>- Grouping by quarter
|Poutcome|No, 4 distinct values|Yes, 'Unknown': 75%|Yes, 'Other': 5%|Not found|Not found|Not found|- One-hot encoding

### Step 2-4: Inspect Boolean Type Columns for Proportional Visualization
|Boolean Column|Imbalance Flag|Class Imbalance|Feature Engineering|
|:---:|:---:|:---:|:---:|
|Default|'False': 98%<br>This is generally reasonable.|'False' has higher deposit rate but < 0.5|No action required|
|Housing|'False': 53%<br>This is generally reasonable.|Yes, 'False' has higher deposit rate > 0.5|No action required|
|Loan|'False': 87%<br>This is generally reasonable.|'False' has higher deposit rate but < 0.5|No action required|



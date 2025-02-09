# SQL-TEKS-Project
SQL TEKS Project: Comparative Analysis of TEKS Across Class Periods
Overview
This project uses SQL and Tableau to analyze trends in student performance across different class periods based on TEKS standards. By identifying patterns in performance, educators can implement targeted interventions to address class-specific needs.
Features
Comparative Analysis: Tracks TEKS performance across class periods.
Trend Monitoring: Uses SQL queries to structure data for Tableau visualizations.
Goal-Setting & Progress Monitoring: Categorizes TEKS mastery levels for easier decision-making.
Focused Analysis: Identifies specific TEKS needing improvement.

Data Analysis Process
1. SQL Query for TEKS Performance Comparison
This query retrieves scores from different assessments and structures the data for trend analysis:
SELECT TEKS, class_pd, 'test_1_5' AS test_name, test_1_5 AS score
FROM teks_tracker_SM1
UNION ALL
SELECT TEKS, class_pd, 'test_1' AS test_name, test_1 AS score
FROM teks_tracker_SM1
UNION ALL
SELECT TEKS, class_pd, 'test_2_5' AS test_name, test_2_5 AS score
FROM teks_tracker_SM1
UNION ALL
SELECT TEKS, class_pd, 'test_2' AS test_name, test_2 AS score
FROM teks_tracker_SM1
UNION ALL
SELECT TEKS, class_pd, 'test_3_5' AS test_name, test_3_5 AS score
FROM teks_tracker_SM1
UNION ALL
SELECT TEKS, class_pd, 'test_3' AS test_name, test_3 AS score
FROM teks_tracker_SM1
ORDER BY TEKS, class_pd, test_name;
2. Visualization: Trend Lines in Tableau
How it Helps:
This data structure allows a clear breakdown of performance by class period and test name.
In Tableau, trend lines with data points reveal class performance over time, identifying consistencies or gaps in understanding.
![SM 1 TEKS Performance Trends by Class Pd](https://github.com/user-attachments/assets/6f9431c7-0be2-4e3e-bb9b-a5d5c473763d)


Goal-Setting and Progress Monitoring
Using SQL, TEKS performance is categorized into four mastery levels:
Mastery Level
Score Range

Mastered
77%-100%

Met
54%-76%

Approached
38%-53%

Not Met
0%-37%

These classifications provide a quick overview of TEKS mastery, helping decide whether to move forward, reteach, or implement interventions.
![SM 1 TEKS Mastry](https://github.com/user-attachments/assets/45edd677-de95-4c85-b2b3-898723eca6c5)


Focused Analysis: Targeted TEKS (e.g., TEKS 8.8C)
This query analyzes a specific TEKS across class periods:
SELECT
    class_pd,
    '8.8C Average' AS measure_name,
    (AVG(test_1_5) + AVG(test_1) + AVG(test_2_5) + AVG(test_2) + AVG(test_3_5) + AVG(test_3)) / 6 AS measure_value
FROM teks_tracker_SM1
WHERE TEKS = '8.8C'
GROUP BY class_pd

UNION ALL

SELECT
    class_pd,
    'Gap to 100' AS measure_name,
    100 - ((AVG(test_1_5) + AVG(test_1) + AVG(test_2_5) + AVG(test_2) + AVG(test_3_5) + AVG(test_3)) / 6) AS measure_value
FROM teks_tracker_SM1
WHERE TEKS = '8.8C'
ORDER BY class_pd, measure_name, measure_value;
Key Insights:
Identifies which classes made the most and least progress toward the 70% benchmark.
Helps adjust instructional strategies per class period.
![8 8C Mastery](https://github.com/user-attachments/assets/62661a89-c69e-47de-a27b-cbf0fb0ecce3)


TEKS Performance Distribution
This query calculates the average TEKS performance per class period:
SELECT
    class_pd,
    TEKS,
    (AVG(test_1_5) + AVG(test_1) + AVG(test_2_5) + AVG(test_2) + AVG(test_3_5) + AVG(test_3)) / 6 AS avg_teks_score
FROM teks_tracker_SM1
GROUP BY class_pd, TEKS;
Visualization:
Box plots in Tableau illustrate TEKS performance spread within class periods.
Median lines show overall TEKS performance for each class.
Outliers highlight high- and low-performing TEKS.
![TEKS Distribution](https://github.com/user-attachments/assets/467af713-455c-4092-b74e-8d1ad76e99c0)


Pros & Cons of the Dashboard
✅ Pros:
Offers detailed insights into TEKS variations across class periods.
Identifies TEKS that drive performance up or down.
Supports data-driven decision-making for interventions.
⚠️ Cons:
Can become cluttered if too many TEKS are analyzed simultaneously.
Requires familiarity with Tableau for in-depth exploration.

## Data Visualization
Check out the interactive Tableau dashbaord
https://public.tableau.com/shared/639MTT5NY?:display_count=n&:origin=viz_share_link 
![TEKS Performance](https://github.com/user-attachments/assets/bfd67bd5-51c2-4f1f-ab9a-e0df602d53aa)


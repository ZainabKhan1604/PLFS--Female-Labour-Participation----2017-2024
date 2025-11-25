# State-wise Trends in Female Labour Force Participation in India (2017–2024) 
## Introduction
The participation of women in the labour market is a key indicator of economic progress and social inclusiveness. The rate of female participation in the labour market is increasing across the world, however India still lags behind even though improvements in female literacy.This persistent gap between education and employment reflects structural, cultural, and economic barriers that constrain women’s participation in paid work. This gap between  education and employment reveals the complex mix of social, structural and economic factors that act as boulders in women’s participation in the workforce. 
**The Periodic Labour Force Survey (PLFS)** was initiated by the _Ministry of Statistics and Programme Implementation (MoSPI)_ in 2017-18 providing an annual measure of labour market outcomes. 
This study used data from 2017-18 till 2023-24 to analyse state-wise trends in the Female Labour Force Participation (FPLF) among women of working age (15-59 years) in India. It further attempts to provide a more comprehensive picture of the state of women’s participation in the paid labour market by using associated indicators like **Female Worker Population Ratio (FWPR)**. Further, it examines the participation of literate females to understand if education translates to higher involvement in the workforce.
## Data and Methodology 
For the purpose of this study, unit level microdata from Periodic Labour Force Survey (PLFS) was used for seven consecutive survey rounds starting from 2017-18 till 2023-24. PLFS remains the primary source of data when it comes to labour markets released by the Ministry of Statistics and Programme Implementation (MoSPI). The data extracted was used to analyse state wise trends in Female Labour Force Participation across years. 
Selected Python code snippets are provided in Appendix A for transparency, while the complete codebase and data processing pipeline are available in the accompanying GitHub repository.
### 2.1) Data Source
For the purpose of this study, person-level data of PLFS was used, which includes detailed information of an individual’s education, marital status, gender and employment. This analysis only uses the Revisit (RV) file for each survey year (eg., hh_per_rv_2017-18, pprv_202-21, etc.). All the data sets were obtained from the microdats.gov.in repository of MoSPI. 
The datasets were imported in .dta (STATA) format to ensure it’s functionality in python’s pyreadstat library. All the variable labels and codes mentioned in the raw data set were verified with the official documents such as Instruction manuals- vol I and II and data layout. 
### 2.2) Sample and Population Scope
    For the purpose of this study only females aged 15-59 years are included which represent the working age female population in India. Males and females not a part of the working age group were excluded from this study. This age group (15-59 years) is in line with the international labour statistics conventions.
This analysis covers 35 States and Union Territories, after making the following adjustments:
**Jammu & Kashmir and Ladakh** : Jammu & Kashmir (code 1) was merged with Ladakh (code 37, introduced in 2021-22) to maintain consistency across all years.
**Dadra & Nagar Haveli and Daman & Diu:** Both were combined for all years under code 25.

### 2.3) Employment Classification
For this analysis  Employment Status was determined using Current Weekly Status (CWS) of each individual. CWS is based on the activity status based on the last 7 days preceding the survey. CWS is preferred in this analysis because it allows consistent comparison across years and reflects short-term employment dynamics.
CWS codes were grouped as follows:
**Employed** : It included all those individuals with CWS codes 11-72 (worked for at least one hour on any day during the reference week.).
**Unemployed**: It included all those individuals with CWS codes 81-82 (Did not work for at least one hour on any day during the reference week but actively seeking or available for work).
**Out of Labour Force**: It included all those individuals with CWS codes 91-98 (Not working and not looking for work).
**Literate Females**: They were defined as those with General Education Level codes between 2-13.
**Illiterate Females**: They were defined as those with General Education Level 1

### 2.4) Data Processing and merging
Data for each survey year was cleaned individually and then merged row-wise using the pandas.concat() function in python. The column names were converted into meaningful labels (eg: state_per_rv to State/UT Code, etc.). Further, all the data sets were filtered to keep only females (Sex = 2) within the age group 15-59 years. 
The final columns kept for the study were: 'Sector', 'State/UT Code', 'Sex', 'Age', 'Marital Status', 'General Edu Level', 'Technical Edu Level', 'Current Weekly Status', 'Industry Code (CWS)', 'Occupation Code (CWS)', 'Sub-sample wise Multiplier' and 'Year'.
A new variable ‘Year_num’ was created to represent the survey year (2017-18, 2018-19, etc.) numerically.
### 2.5) Weighting and Estimation 
State-wise and national level estimates were calculated as per the sampling weights prescribed by MoSPI in the PLFS estimation procedure. The Sub-sample wise multiplier was divided by 100 to come up with the final weight which was applied.


<img width="610" height="127" alt="Screenshot 2025-11-13 224426" src="https://github.com/user-attachments/assets/55698cf8-1df9-467f-a921-29e2e94a397d" />

### 2.6) Indicators Computed
The weighted data was used to derive following indicators :
**FLFP** : (Weighted number of women in labour force {employed + unemployed) / Weighted total women aged 15-59 years) * 100
**FWPR** : (Weighted number of employed women / weighted total women aged 15-59 years) * 100
**FUR** : ( Weighted number of unemployed women / weighted total women aged 15-59 years) * 100

###  2.7) Analytical Tools and Visualisation 
Python was used for all the computations and visualisations. Python libraries such as pandas, numpy, matplotlib and seaborn were used in the Jupyter Notebook. 

### 2.8) Limitations 
Although PLFS covers a rich micro data there a few things that must be noted:
This study only used Current Weekly Status (CWS) which measures only short term labour engagement.
Rural - Urban employment trends and marital status variations are not analysed.
Union Territories like Lakshadweep have a very small population hence even smaller sample size, resulting in small fluctuations.
FLFP was calculated using the Current Weekly Status (CWS) only; hence, estimates may differ from MoSPI’s usual-status figures.
This study doesn’t delve into the sectoral distribution of the female labour force, which is something that could be explored in future work.
This study has not analysed the quality of employment undertaken by individuals, which is something that could be explored in future work.

## Results and Analysis
This study analyzes state level as well as national level trends of Female Labour Force Participation over the years. Moreover, an attempt has been made to analyse the Female Working Population trends and the impact of education on FLFP. Each of these analyses are discussed below.

### 3.1)  National Trends

<img width="2400" height="1500" alt="fplf_india" src="https://github.com/user-attachments/assets/c5b382ad-64eb-46cf-9d4b-c2a4ba1dc625" />

To find out the national trends of FLFP, the micro data of PLFS was filtered to only include women (Sex == 2) of age 15 - 59. FLFP percentage was calculated as the weighted percentage of working age women who were employed or unemployed under Current Weekly Status (CWS). Survey weights were used by dividing the Sub-sample wise multiplier by 100 as recommended by MoSPI. 
This analysis found out that the FLFP was at 20.2748% in 2017-18, which increased slightly to 21.2159 % and 22.487% in 2018-19 and 2019-20 respectively. The COVID years shows a slight dip in FLFP to 22.373% and 22.049% in 2020-21 and 2021-22 respectively. However post COVID years there was a steep recovery to 24.569% in 2022-23 and 26.827% in 2023-24. The estimate of 20.27% in 2017–18 closely aligns with MoSPI’s official CWS figure of 17.5% for women aged 15+, confirming methodological consistency.

### 3.2) State-wise Comparison

<img width="4200" height="1800" alt="1" src="https://github.com/user-attachments/assets/56d6646f-7848-45d9-aa87-4d4718a2f287" />

<img width="4200" height="1800" alt="2" src="https://github.com/user-attachments/assets/a3546fa0-59c7-4c16-8431-b325d88d96f2" />

<img width="4200" height="1800" alt="3" src="https://github.com/user-attachments/assets/49db0dc0-66ad-4996-86d9-34bc701f5578" />

<img width="4200" height="1800" alt="4" src="https://github.com/user-attachments/assets/7a33858c-bf86-42ca-9ee8-65a6ebbbb514" />

<img width="4200" height="1800" alt="5" src="https://github.com/user-attachments/assets/21f5d795-269b-41c6-89bb-cb2884ce34dc" />

<img width="4200" height="1800" alt="6" src="https://github.com/user-attachments/assets/86025795-9c97-4fa5-836f-35fe5294399d" />

<img width="4200" height="1800" alt="7" src="https://github.com/user-attachments/assets/741ed706-4b37-4fa3-afb8-62dfda7ecf1f" />

The state-wise analysis of FLFP reveals exceptional performance of north-eastern states like Sikkim, Meghalaya, Manipur, Mizoram and Nagaland. However states like Uttar Pradesh, Bihar, Rajasthan and Jharkhand continue to remain among the lowest performing states over the years. For contrast, in 2023-24 Nagaland had FLFP of 53.53% whereas the least performing state, Bihar had FLFP of merely 14.66% highlighting the presence of social discrimination , lack of educational and employment opportunities that women continue to face in these states. 
Among the Union Territories Andaman and Nicobar Islands had the highest FLFP throughout while Delhi had the lowest FLFP. In 2023-24, Andaman and Nicobar Islands had FLFP of 46.397% while Delhi stood at only 14.277%.


### 3.3) Female Worker Population Ratio


<img width="3600" height="3000" alt="2017- 2018 (1)" src="https://github.com/user-attachments/assets/bb966ded-deba-42ed-b312-2b919428af18" />

This heatmap shows the Female Worker Population Ratio (FWPR) (15 - 59 age) across States and years (2017-18 to 2023-24). The Female Worker Population Ratio was calculated by taking the weighted number of employed women over weighted total women aged 15-59 years and then multiplied by 100 to get the ratio.
This heat map shows progress of each individual State/UT over the years and the performance of each State/UT in a single sample year. 
This analysis highlights exceptional performance and improvement of north-eastern states over the years especially Nagaland which had FWPR of 11.6 in 2017-18, which became 48.7 in 2023-24. States like Uttar Pradesh, Bihar, Jharkhand and Uttarakhand show little progress over the years with Uttar Pradesh only improving from 10.3 in 2017-18 to 13.8 in 2023-24 reflecting lack of efforts undertaken by these states when it comes to improving employment opportunities to women and removing the social discrimination that women continue face in these states.
The consistently higher participation in northeastern states can be attributed to greater female involvement in agricultural and community-based work, as noted in prior PLFS and NSS reports (MoSPI, 2022).

### 3.4) Education and Participation
<img width="2700" height="1500" alt="Untitled design" src="https://github.com/user-attachments/assets/5bfb29ed-b4ce-4974-aa8f-4cbc31668ad5" />

This chart shows that most women in the working age (15 - 59 years) do not participate in the paid labour force. This could be due to a number of factors ranging from lack of literacy amongst women to the historical social set-up that keeps women within the domestic sphere. Mitali Nikore in her 2022 study concludes, “An analysis of data over the last seven decades shows that women’s work is largely informal, invisible, and labour-intensive.” This highlights the fact that women’s participation in the paid labour market is actively checked by the gender roles that have been assigned to them keeping them engaged in informal and invisible work. 
There is little visible improvement to include more women in the labour force highlighting lack of efforts taken to improve women’s participation.

<img width="2400" height="1500" alt="Untitled design (1)" src="https://github.com/user-attachments/assets/3ef5b869-4dcc-4062-a55c-cee7890d73c7" />

This line chart compares literate females in vs. not in the labour force. Literate females account to women (15 - 59 age) with General Education Level codes between 2-13. Since 2018-19 there is an uptrend in the participation of literate females in the labour force indicating a positive relationship between education and participation. However, the persistent gap indicates that education alone is insufficient without parallel structural and policy changes.


### 3.5) Key Insights
Despite rising literacy and policy push, many educated women remain out of the labour market.
States with higher education or urbanization don’t always have higher FLFP indicating structural barriers (eg. Delhi remains one of the least performing states in FLFP).
North-eastern states except Assam and Arunachal Pradesh have remained among the top performers in FLFP.
COVID years show visible decline followed by recovery.



## 4) Conclusion
Over 2017-18 there has been an improvement in female participation however it remains far below the potential.  Even urbanised states have low participation indicating deep-rooted social and structural barriers. The study also highlights that although female literacy is improving, more women are going to schools and colleges but the gap between education and participation still persists. There is a need for gender-sensitive employment strategies that remain essential for balanced growth.

## 5) References

Ministry of Statistics and Programme Implementation (MoSPI). Periodic Labour Force Survey (PLFS), Annual Reports (2017–2024). Government of India.
MoSPI. Estimation Procedure for PLFS. Government of India, 2023.

Nikore, M. (2022). Women’s Labour Participation in India: A Historical and Policy Analysis. Nikore Associates.
International Labour Organization (ILO). Women at Work Trends 2023.

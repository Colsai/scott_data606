# HHS OIG: Work Products and Reports: Topic Modeling
### Scott Hirabayashi | Summer 2022 (June-August)
### Topic Modeling For Work Scope for HHS OIG (2018-2022)

## Table of Contents   

### PHASE I: Project Proposal & Planning:
<i> June 1, June 8, June 15	</i>
<table>
<tr>
<th> Initial Project Proposal:</th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Project_Proposal.md </th>
<tr>
<th> Final Project Proposal: </th>
<th> https://github.com/Colsai/scott_data606/blob/main/Project_Proposal.md </th>
</table>
  
### PHASE II: Data Preparation & EDA
<i> June 22, June 29, July 6 </i>
<table>
<tr>
<th> EDA </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/data_preparation_eda/Initial_EDA.ipynb </th>
</tr>
<tr>
</tr>
</table>

### PHASE III: Model Training & Deployment 
<i> July 13, July 20, July 27 </i>
<table>
<tr>
<th> Topic Modeling Reports </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Topic_Modeling_Final/Topic_Modeling_Reports_2.ipynb </th>
</tr>
<tr>
<th> Topic Modeling Work Plans </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Topic_Modeling_Final/Topic_Modeling_Workplans_1.ipynb </th>
</tr>
</table>

### PHASE IV: Presentation
<i> July 27- August 2022 </i>
<table>
<tr>
<th> Final Presentation </th> 
<th>https://github.com/Colsai/scott_data606/blob/main/Project_Presentation/HHSOIG_Topic_Modeling.pptx</th>
</tr>
<tr>
<th> Video Presentation </th> 
<th></th>
</tr>
</table>
<hr></hr>

### Introduction





![image info](https://github.com/Colsai/scott_data606/blob/main/hhsoig-banner-logo.png)  
# The Role of HHS OIG: Public Work to Protect US Health Outcomes
## A data-centric approach to analyzing HHS OIG's projects through DHHS OIG Work Plans & Reports (FY2018-Present)

### **Project Focus**  
OIG's mission is to provide objective oversight to promote the economy, efficiency, effectiveness, and integrity of HHS programs, as well as the health and welfare of the people they serve. They outline the primary scope of their work as:

• Safeguarding the Medicare Trust Funds  
• Strengthening Medicaid protections against fraud, waste, and abuse  
• Protecting beneficiaries from prescription drug abuse, including opioids  
• Ensuring health and safety for children served by HHS programs  
• Combatting cybersecurity threats within HHS and healthcare  
• Promoting patient safety and accuracy of payments in home and community settings
• Leveraging technology as it intersects with HHS programs  
• Ensuring HHS managed care and new healthcare models produce value  
• Identifying opportunities to lower prescription drug spending for patients and programs 

The US Department of Health and Human Services- Office of Inspector General (HHS OIG) undertakes valuable work to provide oversight on the larger Department of Health and Human Services in order to protect the American public against fraud, waste and abuse.  
  
This project aims at a textual analysis of the work plans and reports that HHS OIG has produced from FY2018-present, found on the HHS OIG Work Plan ( https://oig.hhs.gov/reports-and-publications/workplan/index.asp)

<blockquote>
<h4> What are work plan items? </h4>
Work plan items are projects that HHS OIG declares to the public for work. Specifically, they are defined as, "...various projects including OIG audits and evaluations that are underway or planned to be addressed during the fiscal year and beyond by OIG's Office of Audit Services and Office of Evaluation and Inspections<sub>5</sub>"  
Each item is After these items are completed, a formal report is drafted and presented to the public. However, these reports only exist in website and .pdf form, making them difficult for larger analysis.
<p> 
<p> However, these work plan items and reports are all public data, and data has been collected on all work plan items from the audit and evaluation teams since 2017. Each of these work plans also have an attached report on the findings: some work plan items have many reports associated, and others have only one.</p>
</blockquote>
 
###  2. Importance and Relevance of Analysis   
The Department of Health and Human Services- Office of Inspector General is the largest inspector general in the United States, and investigates and protects the public from bad actors in the health care sector. More specifically, HHS OIG was established in 1976, to protect the American public from fraud, waste, and abuse, with a central focus on Medicare and Medicaid programs. Healthcare compliance officers, hospitals, and the public are interested in how HHS OIG protects them from issues.   

This oversight is particularly focused on the Medicare and Medicaid programs. 
<blockquote>
<h4> In terms of the scope of these programs: </h4>
<ul>
<li>Medicare alone is the United States' largest health care program- over 60 million American beneficiaries utilize the program<sub>3</sub>. This program cost $829.5 billion dollars (20% of total national health expenditures) <sub>1</sub>.</li>
<li>An additional 87 million US citizens are enrolled in Medicaid/CHIP (Children's Health Insurance Program)<sub>2</sub>. In 2020, Medicaid expenditures equaled $671.2 billion (16% of total national health expenditures)<sub>1</sub> .</li>
<ul>
</blockquote>

There are many avenues for fraud, waste, and abuse, and an extensive analysis of the projects over the past three years provides confidence to medical professionals and the public that HHS OIG is continuing to protect vulnerable populations of people (elderly, low-income, minority groups, all which may be disproportionately affected by fraud/waste/abuse). However, the current work plan that provides data on focus areas is difficult to navigate, and is largely unstructured. This project aims to dissect the HHS OIG's historical work and work patterns, by utilizing text analytics on the OIG work plan, work plan items, and the subsequent reports. 

### 3. Addressed Questions within Project Scope
- What are common themes/trends within the scope of work we can view from looking at the projects that OIG is undertaking? (Locations, focus areas, topics)
- Do we (and how do we) see the influence of major health events, such as COVID, within the scope of OIG's work?
- Do specific types of audits/investigations yield the best ROI? (ROI data and repayment data is included in the unstructured text)?
- How do we connect these outcomes to OIG's priority outcomes and larger mission (*Priority Outcomes: a) Minimizing risks to beneficiaries & b) Safeguarding programs from improper payments and fraud.*)?
  
  ### Additional Questions
1. Are plans (work plans) and findings (reports) similar in terms of topics identified and scope? 
2. How closely do the topics of work identified in the models connect to the priorities outlined by HHS OIG?
3. Are there any topics that appear to be underrepresented from the reports and data?

### 4. Data Sources and Explanation 
- Data sources and explanation can be found at: [https://github.com/Colsai/scott_data606/new/main](https://github.com/Colsai/scott_data606/blob/main/Initial_Data_Source_Description.md)

### 5. Project Units of Analysis
- Scope: OIG's work across the United States (work scope includes DC/Puerto Rico), Time Range: FY2018 (starting 10/17) to June 2022.
- All public OIG **Projects** (work plan items) and their connected **reports**
- Projects defined as: public audits and evaluations, which are performed by separate entities within OIG.
- Reports defined as: reports written after completion of specific analysis performed by a work plan project item.
- Excludes specific or individual investigative actions/arrests (Offive of Investigation data not included)
 
### 6. Variables and Measures Considered
#### Work Plan/Reports Data Elements:
<table>
<tr><th> Titles of work plans (as focus areas)</th><th> Data is included in the work plan</th></tr>
<tr><th> Current status of work plans (Completed, Cancelled, In-Progress) </th><th> Included, but needs standardization/cleaning</th></tr>
<tr><th> Agency focus areas (CMS/FDA/CDC/etc.) </th><th>Included, but needs standardization/cleaning</th></tr>
<tr><th> Expected date of completion for projects </th><th> Data is included in the work plan</th></tr>
<tr><th> Summaries of work projects </th><th> Data is included in the work plan</th></tr>
<tr><th> Summaries of reports </th><th> Data not included in the work plan, separately scraped</th></tr>
<tr><th> Status of items </th><th> Included, but needs standardization/cleaning</th></tr>
</table>
  
**From each of the reports/summaries, I'd also like to pull:**
<table>
  <tr><th> Locations of the analysis</th><th>Would need to be pulled from summaries</th></tr>
  <tr><th> Frequent topics/topic modeling</th><th> Unsupervised model for pulling topics</th></tr>
  <tr><th> Recoveries (in dollar amounts)</th><th>Stretch goal</th></tr>
</table>

### 7. Techniques/models Planned for Project Use(for example, clustering, NLP, ARIMA, etc.)?
#### Techniques and Models:
<table>
<tr><th>Text Analytics </th></tr>
<tr><th> Unstructured NLP for analyzing frequent topics  </th></tr>
<tr><th> Unsupervised text clustering </th></tr>
<tr><th> Dashboard development </th></tr>
</table>

### 8. Initial Schedule and Usage of ML within Project
The main goal initially will be to prototype, clean, and try LDA on the dataset. My biggest focus area here is providing insight into what the data say about OIG's current planned work, and past work.

My method of performance of the models will be to analyze whether extracted themes are logically clear, and then see whether paragraphs appear to match to their corresponding paragraphs. 

### 9. Expected Outcomes
Analyze and provide a holistic look of most-frequent topics of audits and evaluations, and provide analysis on their trending over time. Ultimately, I'd like to use these data sources to create a dashboard product that consolidates the topic modeling in a user-friendly way. The ultimate value of this data is that it is novel. As the coordinator for the current work plan, this product is rarely used to tell a story, and difficult to do so in its current form. By leveraging analytics and NLP techniques, I believe that new insight can be gained into OIG's successes in its work projects.

## Data Model
![](<https://user-images.githubusercontent.com/70355052/182250677-fb1aa06e-fd43-4c9a-8084-362bb56d0a64.png?raw=true>)  
  
<hr></hr>

## References
<sub>1</sub> Budget Basics: Medicare. https://www.pgpf.org/budget-basics/medicare. Accessed 12 June 2022.

<sub>2</sub> February 2022 Medicaid & CHIP Enrollment Data Highlights | Medicaid. https://www.medicaid.gov/medicaid/program-information/medicaid-and-chip-enrollment-data/report-highlights/index.html. Accessed 12 June 2022.

<sub>3</sub> “Medicare Program Is the United State’s Single Largest Health Program.” Health Management Associates, https://www.healthmanagement.com/services/government-programs-uninsured/medicare-program/. Accessed 12 June 2022.

<sub>4</sub> “What You Need to Know About OIG Audits.” Journal of AHIMA, https://journal.ahima.org/page/what-you-need-to-know-about-oig-audits. Accessed 8 June 2022.

<sub>5</sub> Work Plan | Office of Inspector General | U.S. Department of Health and Human Services. https://oig.hhs.gov/reports-and-publications/workplan/index.asp. Accessed 8 June 2022.


![image info](https://github.com/Colsai/scott_data606/blob/main/hhsoig-banner-logo.png)  
# Modeling the Role of HHS OIG: Public Work to Protect US Health Outcomes
## The Value of Topic Modeling For Work Scope for HHS OIG (2018-2022)
### Scott Hirabayashi (under the supervision of Dr. Jay Wang | Summer 2022 (June-August)
<hr></hr>

## **Table of Contents**

* [1. Project Links & Introduction](#introduction)  

* [2. Data Source and Web Scraping](#data-source-and-scraping)

* [3. Exploratory Data Analysis](#eda-and-dataset-analysis)  

* [4. Modeling](#topic-modeling)  

* [5. Project Conclusions](#conclusions)  

* [6. References](#references)  

<hr></hr>

# Introduction
![](<https://user-images.githubusercontent.com/70355052/182250677-fb1aa06e-fd43-4c9a-8084-362bb56d0a64.png?raw=true>)  
<i>An overall picture of the project</i>

<table>
<tr>
<th> Initial/Final Project Proposal</th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Project_Proposal.md </th>
</table>

### **Project Focus**  
OIG's mission is to provide objective oversight to promote the economy, efficiency, effectiveness, and integrity of HHS programs, as well as the health and welfare of the people they serve. They outline the primary scope of their work as:

<blockquote>
<ul>
<li> Safeguarding the Medicare Trust Funds  
<li> Strengthening Medicaid protections against fraud, waste, and abuse  
<li> Protecting beneficiaries from prescription drug abuse, including opioids  
<li> Ensuring health and safety for children served by HHS programs  
<li> Combatting cybersecurity threats within HHS and healthcare  
<li> Promoting patient safety and accuracy of payments in home and community settings
<li> Leveraging technology as it intersects with HHS programs  
<li> Ensuring HHS managed care and new healthcare models produce value  
<li> Identifying opportunities to lower prescription drug spending for patients and programs 
</ul>
</blockquote>

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
  
<hr></hr>

  
# Data Source and Scraping
The text and reports data were taken from the HHS OIG Work Plan, the Office of Inspector General's website that contains all of OIG's publically-declared audits, evaluations/inspections. 
  
<blockquote>
- OIG Work Plans: Contain work scope and focus of work to be undertaken. They connect to specific Reports.
- OIG Reports: Contain Summaries, findings, methodology, and recommendations. They provide a more-specific picture of the work that was accomplished. 
</blockquote>
  
Note:These are summaries of a larger report and communication log that OIG also publishes.
![image](https://user-images.githubusercontent.com/70355052/184550238-7ed029f7-a23d-420e-8b46-d9510b587c68.png)
  
  
Work Plan Scraping was straightforward- scraped the summaries, and any links to connected reports. Reports were more challenging, as OAS and OEI’s websites took longer to find. 

  
![image](https://user-images.githubusercontent.com/70355052/184550128-cb9723ad-3fdb-4085-a08c-389a8fe0255c.png)
  
  
# EDA and Dataset Analysis
<table>
<tr>
<th> EDA </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/data_preparation_eda/OIGworkplan_Initial_EDA.ipynb </th>
</tr>
<tr>
</tr>
</table>

After defining the scope of our corpus as two sets of documents: OIG's work plans and reports, we can proceed with a high-level look of the texts themselves.

## General Information on Work Plan and Reports Datasets:
- Scope: OIG's work across the United States (work scope includes DC/Puerto Rico), Time Range: FY2018 (starting 10/17) to June 2022. The work plan is updated monthly.
- All public OIG **Projects** (work plan items) and their connected **reports**
- Projects defined as: public audits and evaluations, which are performed by separate entities within OIG.
- Reports defined as: reports written after completion of specific analysis performed by a work plan project item.
- Excludes specific or individual investigative actions/arrests (Offive of Investigation data not included)

## EDA on Work Scope
- A majority of work was specifically Centers for Medicare and Medicaid work (415 work plans out of 655).
- OAS work (and therefore, audits), made up about 65% of the total work (423 work plans); OEI work (evaluations and inspections), made up the other 35%. 
- As work plans can recur (and repeat year-to-year), there were duplicates. However, as language and scope of these projects can change year-to-year, duplicates were not removed to retain actual work done.

## EDA on Texts
- Between audits and evaluations, the actual length of texts was similar, as shown:
  ![image](https://user-images.githubusercontent.com/70355052/184555866-cf909c2b-6d72-4612-85b2-0dcc41a85d6d.png)
- Overall, when looking through the tokenized work plans and reports, obvious similarities were present in the scope of analysis:
  <i><center> Top 30 Words, Work Plans </center></i>
![image](https://user-images.githubusercontent.com/70355052/184555881-95d65bf6-23b9-4f4f-87a8-153a2ef5d1ee.png)
  <i><center> Top 30 words, Reports </center></i>
![image](https://user-images.githubusercontent.com/70355052/184555882-de716c68-efe6-4aab-b9f6-212789e4b35b.png)

  
# Topic Modeling
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
  
Two unsupervised topic models were used for topic modeling the two cleaned reports: LDA and BerTopic.
### Latent Dirichlet Allocation (LDA):
The LDA model was created by David Blei, Andrew Ng, and Michael Jordan, is a generative model, but in text mining, it introduces a way to attach topical content to text documents. Each document is viewed as a mix of multiple distinct topics. (Sciencedirect)
  
### BERTopic (LDA): 
BERTopic is a topic modeling technique that leverages BERT embeddings and a class-based TF-IDF to create dense clusters allowing for easily interpretable topics whilst keeping important words in the topic descriptions. (Grootendorst)

  
  
  
## Conclusions 
<th> Final Presentation </th> 
<th>https://github.com/Colsai/scott_data606/blob/main/Project_Presentation/HHSOIG_Topic_Modeling.pptx</th>
</tr>
<tr>  
  
  
  
  
  
  
  
  
  
  
# References
<sub>1</sub> Budget Basics: Medicare. https://www.pgpf.org/budget-basics/medicare. Accessed 12 June 2022.

<sub>2</sub> February 2022 Medicaid & CHIP Enrollment Data Highlights | Medicaid. https://www.medicaid.gov/medicaid/program-information/medicaid-and-chip-enrollment-data/report-highlights/index.html. Accessed 12 June 2022.

<sub>3</sub> “Medicare Program Is the United State’s Single Largest Health Program.” Health Management Associates, https://www.healthmanagement.com/services/government-programs-uninsured/medicare-program/. Accessed 12 June 2022.

<sub>4</sub> “What You Need to Know About OIG Audits.” Journal of AHIMA, https://journal.ahima.org/page/what-you-need-to-know-about-oig-audits. Accessed 8 June 2022.

<sub>5</sub> Work Plan | Office of Inspector General | U.S. Department of Health and Human Services. https://oig.hhs.gov/reports-and-publications/workplan/index.asp. Accessed 8 June 2022.

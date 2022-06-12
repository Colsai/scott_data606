![image info](https://github.com/Colsai/scott_data606/blob/main/hhsoig-banner-logo.png)  
# DATA606: Protecting Modern US Healthcare
### Analysis and Modeling of OIG's projects through DHHS OIG Work Plans and Reports

### **1. What is your issue of interest (provide sufficient background information)?**  
The US Department of Health and Human Services- Office of Inspector General (HHS OIG) undertakes valuable work to provide oversight on the larger Department of Health and Human Services in order to protect the American public against fraud, waste and abuse. This oversight is particularly focused on the Medicare and Medicaid programs. In terms of teh scope of these programs:
- Medicare alone is the United States' largest health care program- over 60 million American beneficiaries utilize the program <sub>1</sub>. This program cost $829.5 billion dollars (20% of total national health expenditures).
- An additional 87 million US citizens are enrolled in Medicaid/CHIP (Children's Health Insurance Program). In 2020, Medicaid expenditures equaled $671.2 billion (16% of total national health expenditures).

With a combination of investigators, auditors, and agents, HHS OIG provides wide-ranging oversight to protect against misuses of these funds. This project aims to dissect the HHS OIG's historical work and work patterns, by utilizing text analytics on the OIG work plan, work plan items, and the subsequent reports. 

#### What are work plan items?

Work plan items are  projects that HHS OIG declares to the public for work. Specifically, they are defined as, "...various projects including OIG audits and evaluations that are underway or planned to be addressed during the fiscal year and beyond by OIG's Office of Audit Services and Office of Evaluation and Inspections<sub>1</sub>"  Each item is After these items are completed, a formal report is drafted and presented to the public. However, these reports only exist in website and .pdf form, making them difficult for larger analysis.

However, these work plan items and reports are all public data, and data has been collected on all work plan items from the audit and evaluation teams since 2017. Each of these work plans also have an attached report on the findings: some work plan items have many reports associated, and others have only one.

### **2. Why is this issue important to you and/or to others?**  
The Department of Health and Human Services- Office of Inspector General is the largest inspector general in the United States, and investigates and protects the public from bad actors in the health care sector. More specifically, HHS OIG was established in 1976, to protect the American public from fraud, waste, and abuse, with a central focus on Medicare and Medicaid programs. Healthcare compliance officers, hospitals, and the public are interested in how HHS OIG protects them from issues.   
- *The work plan can be found at: https://oig.hhs.gov/reports-and-publications/workplan/index.asp.*

There are many avenues for fraud, waste, and abuse, and an extensive analysis of the projects over the past three years provides confidence to medical professionals and the public that HHS OIG is continuing to protect vulnerable populations of people (elderly, low-income, minority groups, all which may be disproportionately affected by fraud/waste/abuse). However, the current work plan that provides data on focus areas is difficult to navigate, and is largely unstructured. 

### **3. What questions do you have in mind and would like to answer?** 
- What are some themes and trends we can view from looking at the projects that OIG is undertaking? (Locations, focus areas, topics)
- Do we (and how do we) see the influence of major health events, such as COVID, within the scope of OIG's work?
- How do we connect these outcomes to OIG's priority outcomes?
*Priority Outcomes*
1. Minimizing risks to beneficiaries & 
2. Safeguarding programs from improper payments and fraud. 
- Do specific types of audits/investigations yield the best ROI? (ROI data and repayment data is included in the unstructured text)

### **4. Where do you get the data to analyze and help answer your questions (creditability of source, quality of data, size of data, attributes of data. etc.)?**  
- HHS OIG displays all public projects, which can be found at https://oig.hhs.gov/reports-and-publications/workplan/.
- The primary challenge is in finding a way to scrape the data. I've initially scraped the paragraphs by writing an initial scraper: 
- https://github.com/Colsai/scott_data606/blob/main/HHSOIG_WP_Scrapers.ipynb

Which scrapes for two data sources:

#### Aggregate-level data
- https://github.com/Colsai/scott_data606/blob/main/Data_Sources/HHS_OIG_Reports.csv
![image](https://user-images.githubusercontent.com/70355052/172527208-be0283b0-512e-49b7-bf5a-820226907e39.png)

#### Reports data
- https://github.com/Colsai/scott_data606/blob/main/Data_Sources/HHS_OIG_workplans.csv
![image](https://user-images.githubusercontent.com/70355052/172527255-2f155ac1-1d6c-4be7-8be7-1c0334cbf247.png)

#### Example of a report (scraped data)
*Data is as it currently is, before cleanup*
![image](https://user-images.githubusercontent.com/70355052/172527504-e34cc318-9858-49fc-b9b8-8d37499ecb9a.png)

*These are not large files (1-2mb), but contain full summary-level data of all reported attributed projects connected to publically-available projects from HHS OIG.*

The major issue with this data is that there is a lot of cleanup and standardization needed. Many of the data elements need to be expanded, such as agency, where acronyms are used- ex. *Food and Drug Administration for one item, FDA for another' Additionally, reports data need several steps of cleanup to make them usable:

### **5. What will be your unit of analysis (for example, patient, organization, or country)? Roughly how many units (observations) do you expect to analyze?**  
- Projects (work plan items) and Reports scraped from HHS OIG website, 2017-Current. OIG's work stretches across the US, and the scope of the work here are audits and evaluations, which are performed by separate entities within OIG.
 
### **6. What variables/measures do you plan to use in your analysis (variables should be tied to the questions in #3)?**  
- Titles of work plans (as focus areas)
- Current status of work plans (Completed, Cancelled, In-Progress)
- Agency focus areas (CMS/FDA/CDC/etc.)
- Expected date of completion for projects
- Summaries of work projects
- Summaries of reports
- Status of items

**From each of the reports, I'd also like to pull from the texts:**
- Locations of the analysis
- Frequent topics/topic modeling
- Recoveries (in dollar amounts)

### **7. What kinds of techniques/models do you plan to use (for example, clustering, NLP, ARIMA, etc.)?**  
- Text Analytics
- Unstructured NLP for analyzing frequent topics
- Unsupervised text clustering
- Dashboard development

### **8. How do you plan to develop/apply ML and how you evaluate/compare the performance of the models?**
My biggest focus area here is providing insight into what the data say about OIG's current planned work, and past work.

### **9. What outcomes do you intend to achieve (better understanding of problems, tools to help solve problems, predictive analytics with practicle applications, etc)?**  
I'm hoping to use this data to analyze and provide a holistic look of most-frequent topics of audits and evaluations, and provide analysis on their trending over time. Ultimately, I'd like to use these data sources to create a dashboard product that consolidates the topic modeling in a user-friendly way. 

The ultimate value of this data is that it is somewhat novel. As the coordinator for the current work plan, this product is rarely used to tell a story, and difficult to do so in its current form. By leveraging analytics and NLP techniques, I believe that new insight can be gained into OIG's successes in its work projects.

<hr>
- *Please use the proposal.md profile for the proposal. Write it in your personal account's repository. After completion and before submission, refresh the contents in the class organization using "Fetch Upstream". Submit the link to the repository in the class organization.*
- *Please make sure it is well formated and styled using Markdown.*
- *We will randomly select a few proposals to walk through during the online session. If you are selected, you will be sharing your proposal and the class will provide feedback.*

## References
<sub>1</sub> Work Plan | Office of Inspector General | U.S. Department of Health and Human Services. https://oig.hhs.gov/reports-and-publications/workplan/index.asp. Accessed 8 June 2022.

“What You Need to Know About OIG Audits.” Journal of AHIMA, https://journal.ahima.org/page/what-you-need-to-know-about-oig-audits. Accessed 8 June 2022.

<sub>2 </sub>https://www.healthmanagement.com/services/government-programs-uninsured/medicare-program/ 

https://www.medicaid.gov/medicaid/program-information/medicaid-and-chip-enrollment-data/report-highlights/index.html

https://www.pgpf.org/budget-basics/medicare#:~:text=Medicare%20accounts%20for%20a%20significant,last%20year%2C%20after%20Social%20Security.

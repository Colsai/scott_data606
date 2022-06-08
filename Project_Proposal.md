![image info](https://github.com/Colsai/scott_data606/blob/main/hhsoig-banner-logo.png)  
# DATA606: Protecting Modern US Healthcare
### Analysis and Modeling of Common Problem Areas through DHHS OIG Data

**1. What is your issue of interest (provide sufficient background information)?**  
I'm interested in understanding more about the Department of Health and Human Services- Office of Inspector General's historical work and work patterns, by utilizing text analytics on the OIG work plan, and work plan items. These work plan items and reports are all public data, and data has been collected on all work plan items from the audit and evaluation teams since 2017. Each of these work plans also have an attached report on the findings: some work plan items have many reports associated, and others have only one.

**2. Why is this issue important to you and/or to others?**  
The Department of Health and Human Services- Office of Inspector General is the largest inspector general in the United States, and investigates and protects the public from bad actors in the health care sector. More specifically, HHS OIG was established in 1976, to protect the American public from fraud, waste, and abuse, with a central focus on Medicare and Medicaid programs. Healthcare compliance officers, hospitals, and the public are interested in how HHS OIG protects them from issues. The work plan can be found at: https://oig.hhs.gov/reports-and-publications/workplan/index.asp.

There are many avenues for fraud, waste, and abuse, and an extensive analysis of the projects over the past three years provides confidence to medical professionals and the public that HHS OIG is continuing to protect vulnerable populations of people (elderly, low-income, minority groups, all which may be disproportionately affected by fraud/waste/abuse). However, the current work plan that provides data on focus areas is difficult to navigate, and is largely unstructured. 

**3. What questions do you have in mind and would like to answer?** 
- What are some themes and trends we can view from looking at the projects that OIG is undertaking? (Locations, focus areas, topics)
- Do we (and how do we) see the influence of major health events, such as COVID, within the scope of OIG's work?

*Priority Outcomes*
1. Minimizing risks to beneficiaries and 
2. Safeguarding programs from improper payments and fraud. 

**4. Where do you get the data to analyze and help answer your questions (creditability of source, quality of data, size of data, attributes of data. etc.)?**  
- HHS OIG displays all public projects, which can be found at https://oig.hhs.gov/reports-and-publications/workplan/.
- The primary challenge is in finding a way to scrape the data. The initial scrape of the data for all projects 

**5. What will be your unit of analysis (for example, patient, organization, or country)? Roughly how many units (observations) do you expect to analyze?**  
- Projects (work plan items) and Reports scraped from HHS OIG website, 2017-Current. OIG's work stretches across the US, and the scope of the work here are audits and evaluations, which are performed by separate entities within OIG.
 
**6. What variables/measures do you plan to use in your analysis (variables should be tied to the questions in #3)?**  
- Titles of work project
- Status of Project (Completed, Cancelled, In-Progress)
- Agency focus areas (CMS/FDA/CDC/etc.)
- Summaries of work projects
- Summaries of reports
- Status of items

From each of the reports, I'd also like to pull:
- Locations
- Frequent topics/topic modeling
- Recoveries (in dollar amounts)

**7. What kinds of techniques/models do you plan to use (for example, clustering, NLP, ARIMA, etc.)?**  
- Text Analytics
- Unstructured NLP for analyzing frequent topics

**8. How do you plan to develop/apply ML and how you evaluate/compare the performance of the models?**  

**9. What outcomes do you intend to achieve (better understanding of problems, tools to help solve problems, predictive analytics with practicle applications, etc)?** - I'm hoping to use this data to analyze and provide a holistic look of most-frequent topics of audits and evaluations, and provide analysis on their trending over time.  

<hr>
- *Please use the proposal.md profile for the proposal. Write it in your personal account's repository. After completion and before submission, refresh the contents in the class organization using "Fetch Upstream". Submit the link to the repository in the class organization.*
- *Please make sure it is well formated and styled using Markdown.*
- *We will randomly select a few proposals to walk through during the online session. If you are selected, you will be sharing your proposal and the class will provide feedback.*

## References
Work Plan | Office of Inspector General | U.S. Department of Health and Human Services. https://oig.hhs.gov/reports-and-publications/workplan/index.asp. Accessed 8 June 2022.

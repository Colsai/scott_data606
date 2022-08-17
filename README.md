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
The Department of Health and Human Services- Office of Inspector General is the largest inspector general in the United States, and investigates and protects the public from bad actors in the health care sector. More specifically, HHS OIG was established in 1976, to protect the American public from fraud, waste, and abuse, with a central focus on Medicare and Medicaid programs. 

Healthcare compliance officers, hospitals, and the public are interested in how HHS OIG protects them from issues.  OIG's mission is to provide objective oversight to promote the economy, efficiency, effectiveness, and integrity of HHS programs, as well as the health and welfare of the people they serve. In their [2020-2025 strategic plan](https://oig.hhs.gov/documents/root/7/OIG-Strategic-Plan-2020-2025.pdf), OIG outline the primary focuses of their current and future work as:

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

This project aims at a textual analysis of the <u> work plans </u> and <u> reports </u> that HHS OIG has produced from FY2018-present, found on the HHS OIG Work Plan ( https://oig.hhs.gov/reports-and-publications/workplan/index.asp)

<h4> What are work plan items? </h4>
Work plan items are projects that HHS OIG declares to the public for addressing in their work; specifically with audits and evaluations and inspections that are performed. These items are identified, approved, posted, and work starts on their scope. Specifically, work plans are defined as, "...various projects including OIG audits and evaluations that are underway or planned to be addressed during the fiscal year and beyond by OIG's Office of Audit Services and Office of Evaluation and Inspections<sub>5</sub>"  
  
<h4> What are reports? </h4>
After elements of a work plan are completed, a formal report is drafted and released to the public. Reports include a rationale, methodology, findings, and recommendations. For the scope of this project, we will focus on the outlined <u> Report-in-Brief (RIB) </u> documents, hereafter referred to as a report, as these summary documents provide valuable summarizations of larger reports.
  
<p> These work plan items and reports are all public data, and data has been collected on all work plan items from the audit and evaluation teams since 2017. Each of these work plans also have an attached report on the findings: some work plan items have many reports associated, and others have only one.</p>
</blockquote>

## Questions within Project Scope
1. What are common themes/trends within the scope of work we can view from looking at the projects that OIG is undertaking?
2. Do we (and how do we) see the influence of major health events, such as COVID, within the scope of OIG's work?
3. How do we connect these plans and outcomes to OIG's priority outcomes and larger mission (see *Project Focus*)
4. Are plans (work plans) and findings (reports) similar in terms of topics identified and scope? 
5. Are there any topics that appear to be underrepresented from the reports and data?
  
<hr></hr>
 
# Data Source and Scraping
In this case, we are looking for two sets of text data: **work plans** and **reports**.

The text and reports data were taken from the HHS OIG Work Plan, the Office of Inspector General's website that contains all of OIG's publically-declared audits, evaluations/inspections. While all active items are available on [HHS OIG Work Plan Active Table](https://oig.hhs.gov/reports-and-publications/workplan/active-item-table.asp), we are looking for all items. After digging into some of the work plan's implementation, we can source this data from utilizing the HTML address patterns for previously-completed items as well as current items.
 
### Work Plan Scraping  
OIG Work Plans: A combination of several data elements- agency, expected date, component, status, title, and summary, work plans are essentially an outline of work scope and focus of work to be undertaken, as well as links/connections to completed **reports**. 

![image](https://user-images.githubusercontent.com/70355052/184550238-7ed029f7-a23d-420e-8b46-d9510b587c68.png) <br>
Work Plan Scraping was straightforward- the summaries were scraped by using a pattern in the HTML address. Each of the work plan html summary pages contain an html table, and a summary. The work plan is easily scraped with Pandas' inbuilt read_html function. 
```
workplan_website = f"https://oig.hhs.gov/reports-and-publications/workplan/summary/wp-summary-{summ_num}.asp"
df = pd.read_html(workplan_website)[0]
```
The one missing data element is the most important, however- the text data. As the summary is within the paragraph tags in the work plan, it is found by using the paragraph tags, concatenated as a single string, then cleaned by replacement.
```
wp_summary = ''.join(str(soup.find_all('p')[3:num_para_elements])).replace("<p>", "").replace("</p>","")[1:-1]
```
In the case of work plans, their 'Report Number(s)' field is a combination of the work plan number, as well as any attributed reports. We can identify reports as:
> - AUDITS/OAS: A-XX-XX-XXXXX (different from their work plan number)
> - EVALUATIONS/OEI: OEI-XX-XX-XXXXX (identical to their work plan number)

These connected numbers are used to generate the reports (See below).

### Report Scraping  
![image](https://user-images.githubusercontent.com/70355052/185025880-f793a586-1d17-4f67-ac71-a7240395055e.png) <br>
OIG Reports: A longer text file, after work is completed and yields results, OIG releases a corresponding report. These reports contain Summaries, findings, methodology, and recommendations. Reports provide a more-specific picture of the work that was accomplished. 

In this case, we are actually looking at Report-in-brief(RIB) documents, presented as active server pages (.asp) on HHS OIG's websites. Essentially, these RIBs are summaries of a larger report and communication log that OIG also publishes, and are more useful as they highlight only key information.

To understand the method of report scraping, all identified work plans and reports were captured using any potential report number as a possible report, then tested against the html address. If the address exists, the corresponding report is scraped. The identified HTML patterns are as follows:
```
OAS_prod_website = f"https://oig.hhs.gov/oas/reports/region{region_num}/{wp_test_num}.asp"
```
```
OEI_prod_website = f"https://oig.hhs.gov/oei/reports/{prod}.asp"
```
Using a similar technique to scraping work plan summaries based on paragraph tags, all existing Reports are added to a pandas dataframe, and exported into .csv.

### Results
These are the total numbers of work plans/reports: <br>  
![image](https://user-images.githubusercontent.com/70355052/184550128-cb9723ad-3fdb-4085-a08c-389a8fe0255c.png)
 
### Text Cleaning/Tokenization
After the work plan scraping was performed, a number of text cleaning steps were performed for preparing the corpuses for both EDA and usage within the LDA model. 
1. Items were tokenized using Regexptokenizer, which removed punctuation within summaries.
```
regex_tokenizer = RegexpTokenizer(r'\w+')
```

2. Work plan/report summaries had stopwords removed: This project used the base NLTK English stopwords list, but additionally included several other words ('on', 'or', etc., and domain-specific words, such as 'oig', 'hhs', as these words did not provide any helpful information for the scope of the topic modeling that followed.

```
tokenized_sums = [[i for i in regex_tokenizer.tokenize(sent) if i not in stopwords] 
                  for sent in wp_init_srs]
```

3. A simple Regex Stemmer was used. Because of many acronyms and domain-specific words, initial tests of modeling with more-restrictive stemmers performed more poorly for topic modeling.

```
Reg_stemmer = RegexpStemmer("ing$|s$|ies$")
tokenized_stemmed_sums = [[Reg_stemmer.stem(word) for word in sent] for sent in tokenized_sums]
```
  
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
- As work plans can recur (and repeat year-to-year), there were duplicates. However, as language and scope of these projects can change year-to-year, duplicates were not removed to retain actual work being completed.

## EDA on Texts
- Reports were noticeably longer in
- Between audits and evaluations, the actual length of texts was similar, as shown:
  ![image](https://user-images.githubusercontent.com/70355052/184555866-cf909c2b-6d72-4612-85b2-0dcc41a85d6d.png)<p></p>
- Overall, when looking through the tokenized work plans and reports, obvious similarities were present in the scope of analysis:
  <i><center> Top 30 Words, Work Plans </center></i>
![image](https://user-images.githubusercontent.com/70355052/184555881-95d65bf6-23b9-4f4f-87a8-153a2ef5d1ee.png)<p></p>
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

The instantiation of each model differs greatly. 

For LDA, text must be cleaned, prepared, and tokenized. In contrast, BERTopic requires little text preparation, and we skip most text cleaning and lemmatization. "In general... you do not need to preprocess your data... keeping the original structure of the text is especially important for transformer-based models to understand the context. (https://github.com/MaartenGr/BERTopic/issues/40)"

However, initial attempts with the BERTopic model on the work plan and reports dataset appeared to occasionally run into issues with clear topics. In this case, we can add a lemmatization/tokenization function through CountVectorizer.

```
#Lemmatizer for cleaning text
class LemmaTokenizer:
    def __init__(self):
        self.wnl = WordNetLemmatizer()
    def __call__(self, doc):
        return [self.wnl.lemmatize(t) for t in word_tokenize(doc)]
#Set docs as workplan summaries
docs = workplan_df["Summary"].reset_index(drop = True)

#Vectorizer model for adding in Stopwords and Lemmatization
vectorizer_model = CountVectorizer(ngram_range=(1, 2), 
                                   stop_words=stopwords,
                                   tokenizer=LemmaTokenizer())
```

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

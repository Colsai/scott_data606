![image info](https://github.com/Colsai/scott_data606/blob/main/hhsoig-banner-logo.png)  
# Utilizing Topic Modeling to Identify Work Priorities at HHS OIG
### Scott Hirabayashi (under the supervision of Dr. Jay Wang)
### DATA606: UMBC Summer 2022 (June-August)  
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

## **Project Focus**  
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

These priorities are of critical importance to HHS OIG- thus, a look at how actual work projects and completed work can shed light on their commitment to each of these separate focus areas. This project aims linking these priorities to NLP-based topic modeling of the <u> work plans </u> and <u> reports </u> that HHS OIG has produced from FY2018-present, found on the HHS OIG Work Plan ( https://oig.hhs.gov/reports-and-publications/workplan/index.asp). To introduce the textual data that will be leveraged:

### What are work plan items? 
Work plan items are projects that HHS OIG declares to the public for addressing in their work; specifically with audits and evaluations and inspections that are performed. These items are identified, approved, posted, and work starts on their scope. Specifically, work plans are defined as, "...various projects including OIG audits and evaluations that are underway or planned to be addressed during the fiscal year and beyond by OIG's Office of Audit Services and Office of Evaluation and Inspections<sub>5</sub>"  
  
### What are reports?
After elements of a work plan are completed, a formal report is drafted and released to the public. Reports include a rationale, methodology, findings, and recommendations. For the scope of this project, we will focus on the outlined <u> Report-in-Brief (RIB) </u> documents, hereafter referred to as a report, as these summary documents provide valuable summarizations of larger reports.
These work plan items and reports are all public data, and data has been collected on all work plan items from the audit and evaluation teams since 2017. Each of these work plans also have an attached report on the findings: some work plan items have many reports associated, and others have only one.</p>
</blockquote>

### What is topic modeling?
Bhutta descripes topic modeling as an unsupervised machine learning technique for scanning documents and determining patterns for clustering by finding word and phrase patterns. These algorithms are considered 'unsupervised', as they do not require training data or preexisting tags (https://www.analyticssteps.com/blogs/what-topic-modelling-nlp). Essentially, topic modeling is a natural language processing technique that ingests text data and returns a logical classification of topics that are frequent across each of the texts, additionally classifying in such a way that texts can have more than one topic.

As the aforementioned work plan and report data we have is untagged and exploratory, topic modeling provides significant opportunity for identifying thematic similarities and *clusters* so that we can extract logic about the major themes of OIG's current work. We will aim to test and leverage two topic modeling algorithms: *Latent Dirichlet Allocation* and *BERTopic* (see [4. Modeling](#topic-modeling)), for making sense of these corpuses of text data.

## Questions within Project Scope
1. What are common themes/trends within the scope of work we can view from looking at the projects that OIG is undertaking?
2. Do we (and how do we) see the influence of major health events, such as COVID, within the scope of OIG's work?
3. How do we connect these plans and outcomes to OIG's priority outcomes and larger mission (see *Project Focus*)
4. Are plans (work plans) and findings (reports) similar in terms of topics identified and scope? 
5. Are there any topics that appear to be underrepresented from the reports and data?
  
<hr></hr>
 
# Data Source and Scraping
<table>
<tr>
<th> Work Plan & Report Scraper </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Scrapers/HHSOIG_WP_Scraper_final.ipynb </th>
</tr>
</table>

To begin our journey into utilizing topic modeling, we are looking for two sets of text data: **work plans** and **reports**. The data for the text and reports data were taken from the HHS OIG Work Plan, the Office of Inspector General's website that contains all of OIG's publically-declared audits, evaluations/inspections. 
  
While all active items are available on [HHS OIG Work Plan Active Table](https://oig.hhs.gov/reports-and-publications/workplan/active-item-table.asp), we are looking for *all items* available on the work plan (publically-facing). After digging into some of the work plan's implementation, we can source this data from utilizing the HTML address patterns for previously-completed items as well as current items with the *requests* and *beautifulsoup* packages. The logic and methodology is explained as follows:
 
## a. Work Plan Scraping  
OIG Work Plans are a combination of several data elements- agency, expected date, component, status, title, and summary. Each work plan is essentially an outline of work scope and focus of work to be undertaken, as well as links/connections to completed **reports**.
![image](https://user-images.githubusercontent.com/70355052/184550238-7ed029f7-a23d-420e-8b46-d9510b587c68.png) <br>
  
Work Plan Scraping is mostly straightforward: the summaries were scraped by using a pattern in the HTML address that was identified by the way that the pages are structured. Each page is individually added in a sequential order from 0 through around 700 (currently). There are some gaps between each summary page number, but this was rectified by testing counts through 750, to ensure that all pages were captured. Each of the work plan html summary pages contain an html table (which contains identifier information), and a text summary, the goal of our scraping for topic modeling. The work plan's html table is easily scraped with Pandas' inbuilt read_html function. 
```
workplan_website = f"https://oig.hhs.gov/reports-and-publications/workplan/summary/wp-summary-{summ_num}.asp"
df = pd.read_html(workplan_website)[0]
```
The one missing data element is the most important, however- the summary text data. As the summary is within the paragraph tags in the work plan, it is found by utilizing bs4 and using the paragraph tags, taking the data within, concatenating it as a single string, then cleaning the html paragraph tags by replacement.
```
wp_summary = ''.join(str(soup.find_all('p')[3:num_para_elements])).replace("<p>", "").replace("</p>","")[1:-1]
```
Another important data element here are the connected reports that are contained within the Report Number(s) field. For work plans, these items also capture any connected work that was completed on the work plan. This is found in each of their 'Report Number(s)' fields, a combination of the work plan number, as well as any attributed reports. We can identify reports as:
*Audits*
> - AUDITS/OAS: A-XX-XX-XXXXX (different from their work plan number)
> - EVALUATIONS/OEI: OEI-XX-XX-XXXXX (identical to their work plan number)

and disregard:
> - AUDITS/OAS: W-XX-XX-XXXXX (W-numbers are only work plans)

After the scrape of each summary page, these report numbers are used to generate the reports through their website addresses (See below). For the full dataset of summaries, these were scraped into .csv format.

## b. Report Scraping  
OIG Reports are longer text files. They are issued after work is completed and yields results, where OIG releases a corresponding report that is added to a work plan (in Report Number(s) field). Rports contain Summaries, findings, methodology, and recommendations, and provide a more-specific picture of the work that was accomplished. In this case, we are actually looking at Report-in-brief(RIB) documents, presented as active server pages (.asp) on HHS OIG's websites. Essentially, these RIBs are summaries of a larger report and communication log that OIG also publishes, and are more useful as they highlight only key information.
  
![image](https://user-images.githubusercontent.com/70355052/185025880-f793a586-1d17-4f67-ac71-a7240395055e.png) <br>
To understand the method of report scraping, all identified work plans and reports were captured using any potential report number as a possible report, then tested against the html addresses for their corresponding procuts. *If* the address exists, the corresponding report is scraped, otherwise it returns as an empty string (""). The identified HTML patterns per websites are as follows:

#### Audit Reports
- ex. https://oig.hhs.gov/oei/reports/OEI-02-20-00490.asp
```
#OAS (Audits) use region number (a part of the A-number code), and the full work plan number
OAS_prod_website = f"https://oig.hhs.gov/oas/reports/region{REGION_NUMBER}/{REPORT_NUMBER}.asp"
```

#### Evaluation/Inspection Reports
- ex. https://oig.hhs.gov/oas/reports/region1/12000508.pdf
```
#OEI numbers simply use the full string
OEI_prod_website = f"https://oig.hhs.gov/oei/reports/{REPORT_NUMBER}.asp"
```
Upon checking the report number against the website, we test whether or not that page exists. While we would expect A-numbers to always have a website, OEI- numbers may not, since the work plan and report number are shared- there is no easy way to know whether or not the report actually exists. Therefore, we test with the *requests* package to see whether or not the website exists before attempting to scrape it. 

If it does, we use similar content identification based on the page tags. In order to prevent issues with overloading the server, we also add a one-second pause per item.
```
response = requests.get(OAS_prod_website)

#If the response is positive, scrape the page.    
if str(response) == '<Response [200]>':
    soup = BeautifulSoup(response.text, 'html.parser')
    wp_item_title = str(soup.find_all('title')[0]).replace('<title>','').replace('</title>','')
    wp_item_summary = str(soup.find_all('p')[5::]).replace("[","").replace("]","").replace("<p>","").replace("</p>","")
    time.sleep(1)
```
This test and attempt at scraping is iterated across the entire set of possible report numbers, then all existing Reports are added to a pandas dataframe. Finally, the file is exported into .csv format.

## Results
**Here are the total numbers of work plans/reports:** <br>  
![image](https://user-images.githubusercontent.com/70355052/184550128-cb9723ad-3fdb-4085-a08c-389a8fe0255c.png)

### Dataset Locations:
<table>
<tr>
<th> Work Plans </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Data_Sources/HHS_OIG_workplans.csv</th>
</tr>
<th> Reports </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/Data_Sources/HHS_OIG_Reports.csv </th>
</tr>
<tr>
</tr>
</table>
 
## c. Text Cleaning/Tokenization
After the work plan scraping was performed, a number of text cleaning steps were performed for preparing the corpuses for both EDA and usage within the LDA model. These steps utilized much of NLTK's in-built text cleaning functionalities, such as English stopwords. The process is as follows:
1. We tokenize items using Regexptokenizer, which removed punctuation within summaries, so that these tokens would not affect the model and be interpreted by the model as a token:
```
regex_tokenizer = RegexpTokenizer(r'\w+')
```

2. We remove stopwords from the work plan/report text data, in order to exclude low/no-meaning words within our corpuses. This project used the base NLTK English stopwords list, but additionally included several other words ('on', 'or', etc., and domain-specific words, such as 'oig', 'hhs', as these words did not provide any helpful information for the scope of the topic modeling that followed. This was to retain only useful language for the model.

```
tokenized_sums = [[i for i in regex_tokenizer.tokenize(sent) if i not in stopwords] 
                  for sent in wp_init_srs]
```

3. We utilize a simple regex stemmer. Because of many acronyms and domain-specific words, initial tests of modeling with more-restrictive stemmers performed more poorly for topic modeling. The Regex stemmer was chosen, as attempts at more-intrusive stemmers appeared to affect the LDA model later on, and it was determined that retaining a simple model (rather than [Snowball Stemmer](https://www.geeksforgeeks.org/snowball-stemmer-nlp/) would perform better for work plan and report topic modeling)

```
Reg_stemmer = RegexpStemmer("ing$|s$|ies$")
tokenized_stemmed_sums = [[Reg_stemmer.stem(word) for word in sent] for sent in tokenized_sums]
```

As we are looking for comparing results across the two models, the same procedures were applied to both the work plans and reports datasets. After these text cleaning steps were performed, we can move on to our Exploratory Data Analysis.

# EDA and Dataset Analysis
After defining the scope of our corpus as two sets of documents: OIG's work plans and reports, we can proceed with a high-level look of the texts themselves. Using Matplotlib/Seaborn, and Wordcloud packages in conjunction with Pandas, we can intuit some high-level insight into the datasets and corpuses.

## EDA on Work Plans
- The 'Announced or Revised' column serves as the status for that item, identifying 266/659 work plans as Completed, and 70 as Completed Partial. From the current work plan website, ~280 items were identified as currently ongoing (changes per month with updates).
- A majority of work plans were specifically for Centers for Medicare and Medicaid work (415 work plans out of 655). Other major agencies that HHS OIG indicated work on included ACF, NIH, FDA, CDC, IHS, and OS. Some items were multi-agency work plans as well.
- OAS work (and therefore, audits), made up about 65% of the total work (423 work plans); OEI work (evaluations and inspections), made up the other 35%. 
- As work plans can recur (and repeat year-to-year), there were duplicates. However, as language and scope of these projects can change year-to-year, duplicates were not removed to retain actual work being completed.
- Any item with that had identical report numbers *was* removed, as this would indicate an exact duplicate. 

## EDA on Reports
- Reports, connected to work plans, were not attached to every work plan. Due to the logic of the numbering system, it is difficult to tell exactly how many work plans are fully complete.

## EDA Insights from Texts
- Between audits and evaluations, the actual length of work plan texts was very similar, as shown:
  ![image](https://user-images.githubusercontent.com/70355052/184555866-cf909c2b-6d72-4612-85b2-0dcc41a85d6d.png)<p></p>
- Reports were noticeably longer (257 total tokens/avg) in textual length than work plans (88 total tokens/avg).

### Visualizing the tokens
Overall, when looking through the tokenized work plans and reports, obvious similarities were present in the scope of analysis:
  <i><center> Top-100 Words, Work Plans </center></i><p></p>
![image](https://user-images.githubusercontent.com/70355052/185027844-fb3bc783-2980-44d9-b0e0-f2faa9f68b4e.png)<p></p>
  <i><center> Top-100 words, Reports </center></i><p></p>
![image](https://user-images.githubusercontent.com/70355052/185027815-c615e356-d08a-4f2d-be53-c2826d2ddfcf.png)<p></p>

A quick glance at these two word clouds identifies how similar the language contained in the work plans and reports appears to be. *Medicare, Medicaid, Hospital, program* and *Provider*, obvious words that connect to OIG's CMS-heavy focus. However, there is some distinguishing language, such as reports containing language highlighting the end-stage of their work, ie *filed report, publication, and reviewed*. In the next step, topic modeling, we'll look at how closely these topics actually are.

A deeper look into the EDA performed on both datasets can be found here:
<table>
<tr>
<th> EDA </th> 
<th> https://github.com/Colsai/scott_data606/blob/main/data_preparation_eda/OIGworkplan_Initial_EDA.ipynb </th>
</tr>
<tr>
</tr>
</table>

# Topic Modeling
As we have defined our data, explored it, and prepared it for modeling, we can begin to use our data within the topic modeling algorithms. In this case, we use two fully-unsupervised topic model algorithms for clustering our topics. 
  
Two unsupervised topic models were used for topic modeling the two cleaned reports: LDA and BerTopic.
#### Latent Dirichlet Allocation (LDA):
The LDA model was created by David Blei, Andrew Ng, and Michael Jordan, is a generative model, but in text mining, it introduces a way to attach topical content to text documents. Each document is viewed as a mix of multiple distinct topics. (Sciencedirect) In this project, we utilize the Gensim package and its LDA functions to capture the topic model for this project.
  
### BERTopic (LDA): 
BERTopic is a topic modeling technique that leverages BERT embeddings and a class-based TF-IDF to create dense clusters allowing for easily interpretable topics whilst keeping important words in the topic descriptions. (Grootendorst) A novel and recent technique, we utilize Grootendorst's extension of the BERT NLP model, created for topic modeling.

## Preparing the Models

### LDA
The preparation steps of each model differs greatly. For LDA, text must be cleaned, prepared, and tokenized. This model is then run against a variable number of topics, chosen optimally by graphing umass coherence score against number of topics. These LDA models use **LdaMulticore**, an optimized Gensim LDA modeling technique for multiple cores (*None* specifes all available cores). Because of the smaller size of the corpus, we modifiy the iterations/passes within the LDAMulticore function- 200 iterations across the dataset was for the iterantions parameter, chosen for better model performance, and 10 passes through.

```
for topic_num in range(1,30,3):
    lda_model = LdaMulticore(corpus=corpus, 
                            id2word=dictionary, 
                            iterations=200, 
                            num_topics=topic_num,
                            workers = None, 
                            passes=10)

    #LDA Model Coherence Score
    cm = CoherenceModel(model=lda_model, 
                        corpus=corpus, 
                        coherence="u_mass")
```

This coherence score is added to a list of values, then displayed to the number of topics.  In the case of the work plans, we chose 17 topics for our LDA topic number for workplans, as umass score appears to spike at this number, and we would expect at least 10 topics (as similar to, or higher than the number of OIG's strategic priorities). <br></br>
![image](https://user-images.githubusercontent.com/70355052/185263656-e5cbdd06-ff20-4385-b0ca-44d44d7e3ccf.png)  

For Reports, we chose **10 topics** for LDA, as a coherence score spike appeared at that topic number.

### BERTopic
In contrast, BERTopic requires little text preparation, and we skip most text cleaning and lemmatization. "In general... you do not need to preprocess your data... keeping the original structure of the text is especially important for transformer-based models to understand the context." (https://github.com/MaartenGr/BERTopic/issues/40)

However, initial attempts with the BERTopic model on the work plan and reports dataset appeared to occasionally run into issues with clear topics. In this case, we can add a lemmatization/tokenization function through CountVectorizer to improve BERTopic from simply throwing the current corpus at the modeling.

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

After running the work plan and reports data through this data preparation stage, we fit the BERTopic model to the data. After the BERTopic model finishes, several in-built packages allow us to logically analyze the results. First, we can test the topics with:

```
#Skip the first element [-1], as the -1 topic captures any non-topic words
bert_model.get_topic_info()[1:]
```

In this case, we can see that the most-common work plan topic was a *medicare,payment,hospital,service...* topic, which is identified in 91 work plans.  
![image](https://user-images.githubusercontent.com/70355052/185267021-af6ee0f7-394e-40f6-854c-e32d0a30399d.png)

We will provide a better picture of information

A full picture of the work can be seen here:
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

## Conclusions 
<table>
<th> Final Presentation </th> 
<th>https://github.com/Colsai/scott_data606/blob/main/Project_Presentation/HHSOIG_Topic_Modeling.pptx</th>
</tr>
<tr>
</table>

Within this project, we performed an end-to-end project for scraping a novel dataset of public work products in order to analyze the larger work scope of the.
  
### Returning to the central questions


### Next Steps

While we were able to create and analyze the initial topic models for the two datasets, we did not push the current model into a web-based environment. Thus, our next steps would be to consider an environment to produce the models in.
  
# References
<sub>1</sub> Budget Basics: Medicare. https://www.pgpf.org/budget-basics/medicare. Accessed 12 June 2022.

<sub>2</sub> February 2022 Medicaid & CHIP Enrollment Data Highlights | Medicaid. https://www.medicaid.gov/medicaid/program-information/medicaid-and-chip-enrollment-data/report-highlights/index.html. Accessed 12 June 2022.

<sub>3</sub> “Medicare Program Is the United State’s Single Largest Health Program.” Health Management Associates, https://www.healthmanagement.com/services/government-programs-uninsured/medicare-program/. Accessed 12 June 2022.

<sub>4</sub> “What You Need to Know About OIG Audits.” Journal of AHIMA, https://journal.ahima.org/page/what-you-need-to-know-about-oig-audits. Accessed 8 June 2022.

<sub>5</sub> Work Plan | Office of Inspector General | U.S. Department of Health and Human Services. https://oig.hhs.gov/reports-and-publications/workplan/index.asp. Accessed 8 June 2022.

### Works Cited

Kapadia, Shashank. “Topic Modeling in Python: Latent Dirichlet Allocation (LDA).” Medium, 29 Dec. 2020, https://towardsdatascience.com/end-to-end-topic-modeling-in-python-latent-dirichlet-allocation-lda-35ce4ed6b3e0.

Kelechava, Marc. “Using LDA Topic Models as a Classification Model Input.” Medium, 6 Aug. 2020, https://towardsdatascience.com/unsupervised-nlp-topic-models-as-a-supervised-learning-input-cf8ee9e5cf28.

Khalid, Irfan Alghani. “Implement Your Topic Modeling Using The BERTopic Library.” Medium, 25 Jan. 2022, https://towardsdatascience.com/implement-your-topic-modeling-using-the-bertopic-library-d6708baa78fe.

“PyLDAvis: Topic Modelling Exploration Tool That Every NLP Data Scientist Should Know.” Neptune.Ai, 16 Nov. 2020, https://neptune.ai/blog/pyldavis-topic-modelling-exploration-tool-that-every-nlp-data-scientist-should-know.

Yadav, Kajal. “The Complete Practical Guide to Topic Modelling.” Medium, 22 Jan. 2022, https://towardsdatascience.com/topic-modelling-f51e5ebfb40a.

## BERTopic Topic Modeling
*BERTopic is a topic modeling technique that leverages 🤗 transformers and c-TF-IDF to create dense clusters allowing for easily interpretable topics whilst keeping important words in the topic descriptions. BERTopic supports guided, (semi-) supervised, and dynamic topic modeling. (MaartgenGr)* 

#### Repo
- https://github.com/MaartenGr/BERTopic

#### Papers
- https://arxiv.org/pdf/2203.05794.pdf
- https://arxiv.org/pdf/2107.02173.pdf

- https://hackernoon.com/nlp-tutorial-topic-modeling-in-python-with-bertopic-372w35l9

#### On removing stopwords:
- https://stackoverflow.com/questions/68127754/removal-of-stop-words-and-stemming-lemmatization-for-bertopic#:~:text=In%20conclusion%2C%20the%20BERTTopic%20does,both%20processing%20time%20and%20results.

#### On Lemmatization
- https://github.com/MaartenGr/BERTopic/issues/286

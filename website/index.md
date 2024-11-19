# Open Voting

## 1. Introduction

In this project, we examine open data in the public domain for two countries: Italy and Russia. Specifically, we focus on the most recent Italian parliamentary election results and the latest Russian presidential election results. These elections represent the most significant political campaigns in their respective countries.

The objectives of our project involve reflecting on the importance and potential issues surrounding open data in the public domain. Through our research, we aim to elucidate the subsequent aspects:

1. **Open Data Limitations**: While the availability of open data is a step towards transparency, it is not sufficient to ensure the integrity of the electoral process. If the underlying procedures are corrupted or problematic, merely publishing the data online does not legitimize the process.

2. **Value of Open Data**: Despite potential corruption, the presence of open data allows for some level of scrutiny. By analyzing the data, we can identify certain manipulations and, to some extent, deduce what the real, uncorrupted results might have been. This highlights the importance of open data in tracing fraud and promoting accountability.

3. **Challenges in Fraud Detection**: While some electoral fraud can be detected and analyzed, other types may remain hidden. Nonetheless, a high degree of certainty about their occurrence can often be established. This underscores that while open data is beneficial, it alone cannot guarantee an unproblematic procedure or a healthy society.

Through our analysis, we aim to illustrate that open data, while not a panacea, is crucial for transparency and accountability in electoral processes.

## 2. Scenario

To achieve our objectives, we collect and analyze electoral data with the finest granularity available. For Italy, we found data at the “comune” (roughly translated as municipality) level (\~94,000 entities) on official websites, resulting in a dataset with (\~117594 rows) for Camera dei deputati, (\~117611 rows) for Senato, which makes a few thousand rows for each commune. For Russia, we accessed data at two levels: individual polling stations (\~94,000 entities) and aggregated data by territorial commissions (\~3,000 rows). For consistency and comparability, we primarily focus on the municipality level of granularity.

Our analysis involves a comprehensive examination of the data to identify anomalies and potential manipulations. We employ statistical methods and data visualization techniques to illustrate our findings. This approach allows us to demonstrate the strengths and limitations of open data in uncovering electoral fraud and promoting transparency.

By the end of this project, we aim to provide a clear understanding of the role of open data in electoral processes, highlighting both its potential and its limitations. This understanding is crucial for developing strategies to enhance transparency and integrity in elections worldwide.

## 3. Original Dataset and Mashup Datasets

### Italy Dataset Overview

**Data Source**:
The dataset for the latest Italian parliamentary election (2022) was obtained from the Official Italian Government Election website, accessible at https://elezioni.interno.gov.it/. It is not clear if it’s more related to the Ministry of the Intern (Ministero dell’Interno) or to the government itself.

**Granularity**:
From a geographical point of view the data is provided at the commune level. The current format presents a challenge as each commune has multiple rows, with each row representing a different candidate. To facilitate analysis, the data needs to be reformatted such that each row corresponds to one commune's electoral results.

**Data Format**:
The available data is provided in spreadsheet format (csv), which has been converted into .txt files for further analysis.

#### Columns Description:

1. **"DATAELEZIONE"** - Date of the election
2. **"CODTIPOELEZIONE"** - Election type code (C for Camera, S for Senato)
3. **"CIRC-REG"** - Regional electoral district
4. **"COLLPLURI"** - Collegio Plurinominale
5. **"COLLUNINOM"** - Colleggio Uninominale
6. **"COMUNE"** - Comune name
7. **"ELETTORITOT"** - Total electorate
8. **"ELETTORIM"** - Male electorate (you can of course infer the Female votants with a simple operation but we found it somehow biased)
9. **"VOTANTITOT"** - Total votes cast
10. **"VOTANTIM"** - Male votes cast
11. **"SKBIANCHE"** - Blank votes
12. **"VOTILISTA"** - Party votes
13. **"DESCRLISTA"** - Party name
14. **"COGNOME"** - Candidate's last name
15. **"NOME"** - Candidate's first name
16. **"LUOGONASCITA"** - Candidate’s place of birth
17. **"DATANASCITA"** - Candidate’s date of birth
18. **"SESSO"** - Candidate’s Sex (described as a binary variable, in some context can be considered not politically correct)
19. **"VOTICANDIDATO"** - Candidate votes’

#### File Structure:
Separate folders are provided for Senate and Camera voting. Notably, in the Camera folder, files include:
- Camera_VAosta_livComune_Scrutini.txt
- Camera_VAosta_LivComune.txt
- Camera_Italia_LivComune.txt

Similarly, in the Senate folder, additional files include:
- Senato_VAosta&Trentino_livComune_Scrutini.txt
- Senato_VAosta&Trentino_LivComune.txt
- Senato_Italia_LivComune.txt

These distinctions might be due to the unique administrative divisions of Valle d'Aosta or some peculiar way of collecting the data they had that made this necessary.

### Russia Dataset Overview

**Data Source**:
The dataset pertains to the latest presidential elections held in Russia in 2024. While the data is theoretically accessible from the Official Russian Government [Election website](http://www.krasnodar.vybory.izbirkom.ru/region/izbirkom?action=show&root=1&tvd=100100339411198&vrn=100100339410030&prver=0&pronetvd=null&region=4&sub_region=4&type=226&report_mode=null), it poses challenges for comprehensive extraction due to website formatting issues and captchas blocking data parsers.

**Complications in Data Retrieval**:
- The data is stored in separate HTML tables for each polling station or 'municipal aggregation'/'territorial commission' of polling stations.
- Captchas and minor formatting techniques hinder automated data parsing efforts.
- Original websites accessible only from Russian IP addresses 

**Data Collection Method**:
Given the challenges in accessing raw data, a dataset compiled by Russian independent electoral data analyst Ivan Shukshin is utilized for analysis. This dataset was disseminated via the 'Non-elections (rus. Невыборы)' telegram channel and gained widespread attention across Russian and international media platforms.

#### Dataset Composition:
The dataset consists of multiple .csv files:
1. **Polling Station Level Data**: Granularity at the level of individual polling stations.
2. **Territorial Commission Level Data**: Aggregated data covering several polling stations within a 'territorial commission,' roughly equivalent to a municipality.
3. **Regional Level Data**: Data aggregated at the regional level.
4. **Remote Voting Data**: Data pertaining to remote voting, where votes were registered online rather than on paper ballots.

#### Focus and Analysis:
The primary focus is on the second file (Territorial Commission Level Data) to maintain consistency with the granularity of the Italian dataset. However, a closer examination of the first file (Polling Station Level Data) may be necessary to detect specific anomalies or irregularities.

#### Description of Columns:
The second file (Territorial Commission Level Data) includes the following columns (in Russian):
- **region**: Region name
- **tik**: Territorial commission name
- **Число избирателей, включенных в список избирателей**: Number of voters included in the voter list
- **Число избирательных бюллетеней, полученных участковой избирательной комиссией**: Number of ballots received by the precinct election commission
- **...** (other columns not translated)

### Mashup Datasets we obtained and managed


# 4. Quality Analysis of the Datasets

**Italy**:
- **Accuracy**: Validate vote counts, candidate names, and other key data points against official records.
- **Consistency**: Ensure uniformity in data entry and formatting across communes.
- **Completeness**: Check that all necessary information is included and that no data points are missing.

**Russia**:
- **Accuracy**: Compare polling station-level data with aggregated data by territorial commissions to detect discrepancies.
- **Consistency**: Standardize data formats and entries across polling stations and territorial commissions.
- **Completeness**: Verify the inclusion of all relevant data points and ensure no omissions.

# 5. Legal Analysis

Italy:

**Privacy**:
The only real issue with Italian data is related to municipalities with too few inhabitants, from this dataset it is possible to infer with a high probability voting trends, some cases are evident like Monterone with a population of 34. In general Municipalities with 100 or less inhabitants are 70 in Italy, this can, in fact, represent a major privacy issue that goes against the art. 48 of the Italian Constitution, that protects the privacy of the vote.

>- Ensure that any personal data in the datasets is anonymized to comply with GDPR regulations.
>- Review the legal frameworks governing data privacy in Italy and Russia.

**Licensing**:
The License in Italy is, unexpectedly, not clear. The platform we used, the one that provides the general dataset for the elections just labels the collection as “Open Data”, on the other hand with a more accurate research we were able to find another page called “dati.gov.it” that contains Electoral data on the municipality and regional level. Each municipality probably released their data in different open data formats on this website, while the eligendo website published the mashup dataset. 
In “dati.gov.it” we’re able to find a page dedicated to the IODL (Italian Open Data License), our datasets are not explicitly released under this license, but we can infer that they probably are if we consider that both websites are part of the Governement web domain.

**Purpose**:
Italy is a member of the EU and the Open Data release is probably part of the current implementation of the EU directives on this subject.
In general Italy is considered a democratic country and the release of this kind of data is public interest and in general a fair and good practice.

> Russia:

# 6. Ethics Analysis

Italy:

This is a very institutional datasets, related to the most important moment of a functioning democracy, it records a very large audience and the data collection must be as secret and anonymous as possible in full respect of the Italian Constitution. Nevertheless it’s possible to trace and identify some prejudices and biases that affect the way the dataset is designed, the most problematic are related to sex and gender:
the choice of recording the “gender” of the candidate as a binary variable (M/F) is certainly not free of concerns in an everchanging cultural and social landscape 
Same goes with the distinction of male voters from the total (we have two columns, one for total votes, the other recording male votes). In this case we need a further task (a simple subtraction) to find the correct number of female voters and yet it’s not justifiable stating that another column would’ve been cumbersome for the dataset. If we always need a further task, why not inferring the total voters number by the sum of male and female voters?

**Discrimination**:
- Ensure that the data does not lead to unfair treatment of any group based on ethnicity, gender, or other factors.

**Cognitive Bias**:
- Identify and mitigate any biases present in the data, especially those related to data collection and reporting.

**Prejudice**:
- Ensure the data is not used to reinforce existing prejudices or stereotypes.

# 7. Technical Analysis (Formats, Metadata, URI, Provenance)

Italy:

The file extension for the italian dataset is .txt, probably to allow easier interoperability and readability on any machine. The format is a csv that uses semi-columns (;) as separators, this latter choice is odd, because it is not the most common way of separating cells in a csv and can lead to some errors during import and reading in certain analysis context.
The metadata is scarce and not adequate for a dataset that carries this prominence, it’s not easy to find column descriptions that allow us to immediately understand the content, leading to time consuming inference tasks.
There’s no real URI because the files are published as downloadable .zip archives (we will provide a URI for the raw files uploading them on github).
The provenance is not stated, all we know is that the website is inserted in the government web domain, so it’s at least trustable. 


**Formats**:
- Discuss the data formats used (e.g., CSV, JSON) and their interoperability.

**Metadata**:
- Ensure comprehensive metadata is available, describing the structure, source, and characteristics of the data.

**URI**:
- Discuss the use of Uniform Resource Identifiers to ensure persistent access to the data.

**Provenance**:
- Trace the origin and history of the datasets, documenting how they were collected and processed.

# 8. Sustainability of the Update of the Datasets Over Time

Italy:
Being the elections clearly positioned in time the website is able to be constantly up to date with all the different elections that take place in Italy each year (the website serves as platform to get data about all kind of elections that take place on national territory).


**Update Mechanisms**:
- Describe the processes for updating the datasets with new information as it becomes available.

**Sustainability**:
- Discuss strategies to ensure the continuous availability and relevance of the data, including regular updates and maintenance.

# 9. Visualization and Analysis

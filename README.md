# Cleverly Multilingual Email Zoning Corpus

New annotated multilingual email zoning corpus, containing:
- Gmane email corpus annotated by email zones
- 215 French emails
- 210 Potuguese emails
- 200 Spanish emails


## Table of contents

1. [Files and folders](#files) 
2. [Reference](#paper)
2. [Licence](#licence)
3. [Corpus description](#corpus)
    1. [Email zones](#zones)
    2. [Statistics](#stats)
    3. [Annotation format](#annotations)   
4. [How to use Cleverly Zoning Corpus](#howto)
    1. [Load the email textual content](#load_corpus) 
    2. [Load Cleverly corpus and match Ids (Python)](#macth_ids) 


## Files and folders  <a id="files"></a>

```
├── README.md                     --
├── code/                         --
├── corpus/                       --
│   ├── es_annotator1.txt   -- 
│   ├── fr_annotator.txt   -- 
│   └── pt_zone_annotations.txt   --
└── paper/                        --
```

## Reference  <a id="paper"></a>
If you use this corpus, please cite the original paper: 

> Bruno Jardim, [Ricardo Rei](https://www.linkedin.com/in/ricardo-rei-159154172/) and [Mariana S. C. Almeida](https://www.linkedin.com/in/marianaalmeida/). 
> ["Multilingual Email Zoning"](https://arxiv.org/abs/2102.00461).
> [EACL 2021 student Research Wrokshop](https://www.aclweb.org/portal/content/eacl-2021-student-research-workshop-second-call-papers), April 2021.

with the bibtex:

```
@inproceedings{BJardim2021,
 author = {Bruno Jardim and Ricardo Rei and Mariana S. C. Almeida},
 title = {Multilingual Email Zoning},
 booktitle = {EACL 2021 student Research Wrokshop},
 publisher = {Association for Computational Linguistics},
 year = {2021},
 month = {April},
 location = {online},
 url = {https://arxiv.org/abs/2102.00461},
} 
```


### Abstract <a id="abstract"></a>
>The segmentation of emails into functional zones (also dubbed **email zoning**) is a relevant preprocessing step for most NLP tasks that deal with emails. However, despite the multilingual character of emails and their applications, previous literature regarding email zoning corpora and systems was developed essentially for English. In this paper, we analyse the existing email zoning corpora and propose Cleverly zoning corpus,
a new multilingual benchmark composed of 625 emails in Portuguese, Spanish and French. Moreover, we introduce Okapi, the first multilingual email segmentation model based on a language agnostic sentence encoder. Besides generalizing well for unseen languages, our model is competitive with current English benchmarks, and reached new state-of-the-art performances for domain adaptation tasks in English.

## Licence  <a id="licence"></a>

Apache License 2.0.
See more details are in the LICENCE file in the root of this project.


## Corpus description  <a id="corpus"></a>
To build a multilingual email corpus, we searched the [Gmane corpus] (Bevendor et al., 2020) for Portuguese, Spanish and French emails. Then, following the classification schema proposed in Bevendor et al. (2020), we produced a total of 625 annotated emails that compose the Cleverly Email Zoning Corpus.

### Email zones <a id="zones"></a>

- **paragraph**: main content; new content from the current email sender.
- **closing**: content that closes the email (ex: Regards, Some Name).
- **inline_headers**: contain lines from information that is used to contextualize the details of a previous message in the thread, such as addresses, dates, recipients, etc.
- **log_data**: contain information about configurations or events that have occurred within a software application like error messages or loading of files.
- **mua_signature**: include legal disclaimers, privacy statements, or other automatically generated texts advising the people that interact with the email. Also contained under MUA signature are automatically generated message lines that define from which device the email was sent, mail user agen and mailing list details or advertisements (e.g. Sent from iPhone).
- **patch**: contain text with pieces of code used to make changes to a computer program or its supporting data in order to update, fix, or improve it. This includes fixing security vulnerabilities and other bugs (source code diffs).
- **personal_signature**: consider content containing contact or other personal information such as name, job title, company, phone number, etc., that is automatically inserted at the end of an email message.
- **quotation**: include contents quoted from previous messages in the same conversation thread and forwarded content from other conversations. Each line typically starts with a “>”.
- **quotation_marker**: initiate quotation zones stating the quotation author and date of a quotation.
- **raw_code**: contain text regarding code being developed in any programming languages (source code).
- **salutation**:  contain the terms of address and recipient names at the beginning of a message.
- **section_heading**:  lines that are headers of other zones, mainly of paragraph zone. 
- **tabular**: text in a semi-structured tabular or matrix format.
- **technical**: contain lines of automatic messages generated by Gmane regarding initiation, ending or elimination of email parts; inline attachments or PGP signatures.
- **visual_separator**: lines with no alphanumeric characters, used to divide the text between multiple zones.

### Statistics <a id="stats"></a>

While French is the language with more emails, Portuguese and Spanish emails tend to be longer, resulting in a greater amount of lines and an overall higher number of zones per email. 
The distribution of zones is quite similar between the three languages, with the percentage of the total lines being: quotation (52.2\% of the all the corpus' lines), paragraph (19.8\%), MUA signature (8.8\), personal signature (3.7\%), visual separator (2.7\%), quotation marker (2.7\%),closing ($2.5\%$), raw code ($2.0\%$), inline headers (1.9\%), salutation (1.0\%), tabular (0.4\%), technical (0.3\%), patch (0.2\%) and section heading (0.1\%). Spanish and French tickets do not contain any section heading lines.

|  | **pt** | **es** | **fr** |
| ------ | ------ | ------ | ------ |
| emails | 210 | 200 | 215 |
| zones | 15 | 14 | 14 |
| lines | 12366 | 9824  | 6958 |
| lines per email | 58.9 | 49.1 | 32.4 |
| zones per email | 8.6 | 6.5 | 5.9 |

The annotation was carried out on [Tagtog] by two annotators - one native Portuguese speaker and the other native Spanish speaker, both with academical background in French and fluent in the third language. Each email was annotated by both annotators. The Inter-annotator agreement is the following:

|  | **pt** | **es** | **fr** |
| ------ | ------ | ------ | ------ |
|F<sub>1</sub> A<sub>1</sub>A<sub>2</sub>| 0.93 | 0.92 | 0.96 |
|F<sub>1</sub> A<sub>2</sub>A<sub>1</sub>| 0.94 | 0.92 | 0.96 |
|*k* (Cohen's Kappa) | 0.90 | 0.87 | 0.94 |



### Annotation format  <a id="annotations"></a>
The corpus comes is divided in three files (one per language), each containing a list of dictionaries. Each email annotation (one dictionary) consists of two key value pairs:

```sh
{"_id": "<urn:uuid:aa5e973e-65fc-4d32-a0d1-7848eaf405e8>", "zones": [["salutation", 0, 11], ["paragraph", 11, 601], ["closing", 601, 610], ["personal_signature", 610, 677], ["mua_signature", 677, 759], ["quotation_marker", 759, 829], ["quotation", 829, 1150]]}
```
The first key value pair "_id" is the email id from the original [Gmane corpus].
The second key value pair "zones" contains the annotated zone spans as a list of lists. Each sublist containing the name of the zone, starting character and ending character. 


## How to use Cleverly Zoning Corpus <a id="howto"></a>

### Load the email textual content  <a id="load_corpus"></a>
To retrieve the email content:

1. Request access to the full Gmane corpus from: https://webis.de/data/webis-gmane-19.html

2. Download the **webis-gmane-19-part04 folder**

3. Access the **.ndjson file part-0051**

4. Retrive the **first 300000 emails**. (See instructions about how to extract file content from: https://webis.de/data/webis-gmane-19.html and [Gmane README.md])

5. Match ids with our zone annotations

### Load Cleverly corpus and match Ids (Python)  <a id="macth_ids"></a>

#### Open Cleverly corpus files
Open one of the annotation files (french)

```python
import io
import json
with io.open('fr_zone_annotations.json', encoding="utf-8") as json_file:
    cleverly_fr = json.load(json_file)
```    

#### Match Cleverly ids with the ones from the full Gmane corpus to get email text
After requesting for access to the full Gmane corpus (as outlined before), open the **part-0051.ndjson** file and extract the **first 3000000** lines
```python
gmane = []
for line in open('webis-gmane-19-part04\part-0051.ndjson', 'r', encoding="utf-8"):
    while len(gmane)<=3000000:
        gmane.append(json.loads(line))
```
Reassemble ids and email content
```python
gmane_id_email = []
for j, line in enumerate(gmane):
    if j%2==0:
        _id = line['index']['_id']
    else:
        dic = {'_id': _id, 'lang': line['lang'], 'text': line['text_plain']}
        gmane_id_email.append(dic)
        dic = {}  
```
 
 Filter for correct language
 ```python
gmane_fr = []
for email in gmane_id_email:
    if email['lang'] == 'fr':
        gmane_fr.append(email)
```
Match ids
```python
fr_email_zones = []
for g_mail in gmane_fr:
    for c_ann in cleverly_fr:
        if g_mail['_id'] == c_ann['_id']:
            fr_email_zones.append((c_ann['_id'], g_mail['text'], c_ann['zones']))

```

[Gmane corpus]:https://webis.de/data/webis-gmane-19.html
[Tagtog]: Tagtog.net/#
[Gmane README.md]: https://github.com/webis-de/acl20-crawling-mailing-lists/blob/master/README.md


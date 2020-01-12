---
title:  "Search at scale"
date:   2017-11-18 10:00:00 -0500
categories: Tech
toc: true
toc_label: "On this page"
toc_icon: "list"
excerpt: "What every software engineer should know about search"
---

##### A collection of insights and resources that could help you to build search experiences

[TOC]

## Search is an inherently messy problem:

1. Queries are highly variable. 

2. The search problems are highly variable based on product needs.

3. Think about how different Facebook search (searching a graph of people),

   YouTube search (searching individual videos), Or how different both of those are are from Kayak (air travel planning is a really hairy problem).

4. Google Maps (making sense of geo-spacial data).

5. Pinterest (pictures of a brunch you might cook one day).


<u>**Note:**</u> 

1. Search is not just about building software that does ranking or retrieval for a specific domain. Search systems are usually an evolving pipeline of components that are tuned and evolve over time and that build up to a cohesive experience.
2. The key to success in search is building processes for evaluation and tuning into the product and development cycles. A search system architect should think about processes and metrics, not just technologies.
3. ❗️Even if you are using an existing open source or commercial solution, you should have some sense of the **complexity of the search problem** and where there are likely to be pitfalls.
4. **Named-entity recognition**
   Named-entity recognition (NER) (also known as entity identification, entity chunking and entity extraction) is a subtask of information extraction that seeks to locate and classify named entities in text into pre-defined categories such as the names of persons, organizations, locations, expressions of times, quantities, monetary values, percentages, etc.
5. **Locality-sensitive hashing (LSH)** reduces the dimensionality of high-dimensional data. LSH hashes input items so that similar items map to the same “buckets” with high probability (the number of buckets being much smaller than the universe of possible input items). LSH differs from conventional and cryptographic hash functions because it aims to maximize the probability of a “collision” for similar items.

**Search is different for every product, and choices depend on many technical details of the requirements. It helps to identify the key parameters of your search problem:**

1. Size: How big is the corpus (a complete set of documents that need to be searched)? Is it thousands or billions of documents?
2. Media: Are you searching through text, images, graphical relationships, or geospatial data?
3. 🔷 Corpus control and quality: Are the sources for the documents under your control, or coming from a (potentially adversarial) third party? Are all the documents ready to be indexed or need to be cleaned up and selected?
4. Indexing speed: Do you need real-time indexing, or is building indices in batch is fine?
5. Query language: Are the queries structured, or you need to support unstructured ones?
6. Query structure: Are your queries textual, images, sounds? Street addresses, record ids, people’s faces?
7. Context-dependence: Do the results depend on who the user is, what is their history with the product, their geographical location, time of the day etc?
8. Suggest support: Do you need to support incomplete queries?
9. Latency: What are the serving latency requirements? 100 milliseconds or 100 seconds?
10. Access control: Is it entirely public or should users only see a restricted subset of the documents?
11. Compliance: Are there compliance or organizational limitations?
12. Internationalization: Do you need to support documents with multilingual character sets or Unicode? (Hint: Always use UTF-8 unless you really know what you’re doing.) Do you need to support a multilingual corpus? Multilingual queries?



## Search Pipeline problems

### 1. Index selection:

given a set of documents (e.g. the entirety of the Internet, all the Twitter posts, all the pictures on Instagram), select a potentially smaller subset of documents that may be worthy for consideration as search results and only include those in the index, discarding the rest. This is done to keep your indexes compact, and is almost orthogonal to selecting the documents to show to the user. Examples of particular classes of documents that don’t make the cut may include:

#### a. Spam:

oh, all the different shapes and sizes of search spam! A giant topic in itself, worthy of a separate guide. A good web spam taxonomy overview.

#### b. Undesirable documents:

domain constraints might require filtering: porn, illegal content, etc. The techniques are similar to spam filtering, probably with extra heuristics.

#### c. Duplicates:

Or near-duplicates and redundant documents. Can be done with Locality-sensitive hashing, similarity measures, clustering techniques or even clickthrough data. A good overview of techniques.

#### d. Low-utility documents:

The definition of utility depends highly on the problem domain, so it’s hard to recommend the approaches here. Some ideas are: it might be possible to build a utility function for your documents; heuristics might work, or example an image that contains only black pixels is not a useful document; utility might be learned from user behavior.



### 2. Index construction:

For most search systems, document retrieval is performed using an inverted index — often just called the index.

- The index is a mapping of search terms to documents. A search term could be a word, an image feature or any other document derivative useful for query-to-document matching. The list of the documents for a given term is called a posting list. It can be sorted by some metric, like document quality.

- Figure out whether you need to index the data in real time.❗️Many companies with large corpora of documents use a batch-oriented indexing approach, but then find this is unsuited to a product where users expect results to be current.

- With text documents, term extraction usually involves using NLP techniques, such as stop lists, stemming and entity extraction; for images or videos computer vision methods are used etc.

- In addition, documents are mined for statistical and meta information, such as references to other documents (used in the famous PageRank ranking signal), topics, counts of term occurrences, document size, entities A mentioned etc. That information can be later used in ranking signal construction or document clustering. Some larger systems might contain several indexes, e.g. for documents of different types.

- Index formats. The actual structure and layout of the index is a complex topic, since it can be optimized in many ways. For instance there are posting lists compression methods, one could target mmap()able data representation or use LSM-tree for continuously updated index.

  

## Query analysis and document retrieval:

Most popular search systems allow non-structured queries. That means the system has to extract structure out of the query itself. In the case of an inverted index, you need to extract search terms using NLP techniques.
The extracted terms can be used to retrieve relevant documents. Unfortunately, most queries are not very well formulated, so it pays to do additional query expansion and rewriting, like:

- [Term re-weighting](http://orion.lcg.ufrj.br/Dr.Dobbs/books/book5/chap11.htm).
- [Spell checking](http://norvig.com/spell-correct.html). Historical query logs are very useful as a dictionary.
- [Synonym matching](http://nlp.stanford.edu/IR-book/html/htmledition/query-expansion-1.html). Another survey.
- [Named entity recognition](https://en.wikipedia.org/wiki/Named-entity_recognition). A good approach is to use HMM-based language modeling.
- Query classification. Detect queries of particular type. For example, Google Search detects queries that contain a geographical entity, a porny query, or a query about something in the news. The retrieval algorithm can then make a decision about which corpora or indexes to look at.
- Expansion through personalization or local context. Useful for queries like “gas stations around me”.



## Ranking:

Given a list of documents (retrieved in the previous step), their signals, and a processed query, create an optimal ordering (ranking) for those documents.

- Originally, most ranking models in use were hand-tuned weighted combinations of all the document signals. Signal sets might include PageRank, clickthrough data, topicality information and others.
- To further complicate things, many of those signals, such as PageRank, or ones generated by statistical language models contain parameters that greatly affect the performance of a signal. Those have to be hand-tuned too.
- Lately, 🔷 learning to rank, signal-based discriminative supervised approaches are becoming more and more popular. Some popular examples of LtR are McRank and LambdaRank from Microsoft, and MatrixNet from Yandex.
- A new, vector space based approach for semantic retrieval and ranking is gaining popularity lately. The idea is to learn individual low-dimensional vector document representations, then build a model which maps queries into the same vector space.
- Then, retrieval is just finding several documents that are closest by some metric (e.g. Eucledian distance) to the query vector. Ranking is the distance itself. If the mapping of both the documents and queries is built well, the documents are chosen not by a fact of presence of some simple pattern (like a word), but how close the documents are to the query by meaning.

## Indexing pipeline operation

Usually, each of the above pieces of the pipeline must be operated on a regular basis to keep the search index and search experience current.

- ❗️Operating a search pipeline can be complex and involve a lot of moving pieces. Not only is the data moving through the pipeline, but the code for each module and the formats and assumptions embedded in the data will change over time.
- A pipeline can be run in “batch” or based on a regular or occasional basis (if indexing speed does not need to be real time) or in a streamed way (if real-time indexing is needed) or based on certain triggers.
- Some complex search engines (like Google) have several layers of pipelines operating on different time scales — for example, a page that changes often (like cnn.com) is indexed with a higher frequency than a static page that hasn’t changed in years.



## ==Serving systems==

Ultimately, the goal of a search system is to accept queries, and use the index to return appropriately ranked results. While this subject can be incredibly complex and technical, we mention a few of the key aspects to this part of the system.

1. **Performance:** users notice when the system they interact with is laggy. ❗️Google has done extensive research, and they have noticed that number of searches falls 0.6%, when serving is slowed by 300ms. They recommend to serve results under 200 ms for most of your queries. A good article on the topic. This is the hard part: the system needs to collect documents from, possibly, many computers, than merge them into possible a very long list and then sort that list in the ranking order. To complicate things further, ranking might be query-dependent, so, while sorting, the system is not just comparing 2 numbers, but performing computation.
2. 🔷 **Caching results:** is often necessary to achieve decent performance. ❗️ But caches are just one large gotcha. The might show stale results when indices are updated or some results are blacklisted. Purging caches is a can of worms of itself: a search system might not have the capacity to serve the entire query stream with an empty (cold) cache, so the cache needs to be pre-warmed before the queries start arriving. Overall, caches complicate a system’s performance profile. Choosing a cache size and a replacement algorithm is also a challenge.
3. **Availability:** is often defined by an uptime/(uptime + downtime) metric. When the index is distributed, in order to serve any search results, the system often needs to query all the shards for their share of results. ❗️That means, that if one shard is unavailable, the entire search system is compromised. The more machines are involved in serving the index — the higher the probability of one of them becoming defunct and bringing the whole system down.
4. **Managing multiple indices:** Indices for large systems may separated into shards (pieces) or divided by media type or indexing cadence (fresh versus long-term indices). Results can then be merged.
5. **Merging results of different kinds:** e.g. Google showing results from Maps, News etc.



## Quality, evaluation, and improvement

So you’ve launched your indexing pipeline and search servers, and it’s all running nicely. Unfortunately the road to a solid search experience only begins with running infrastructure.

Next, you’ll need to build a set of processes around continuous search quality evaluation and improvement. In fact, this is actually most of the work and the hardest problem you’ll have to solve.

🔷 **What is quality?** First, you’ll need to determine (and get your boss or the product lead to agree), what quality means in your case:

1. Self-reported user satisfaction (includes UX)
2. Perceived relevance of the returned results (not including UX)
3. Satisfaction relative to competitors
4. Satisfaction relative performance of the previous version of the search engine (e.g. last week)
5. User engagement

**Metrics:** Some of these concepts can be quite hard to quantify. On the other hand, it’s incredibly useful to be able to express how well a search engine is performing in a single number, a quality metric.
Continuously computing such a metric for your (and your competitors’) system you can both track your progress and explain how well you are doing to your boss. Here are some classical ways to quantify quality, that can help you construct your magic quality metric formula:

1. Precision and recall measure how well the retrieved set of documents corresponds to the set you expected to see.
2. F score (specifically F1 score) is a single number, that represents both precision and recall well.
3. Mean Average Precision (MAP) allows to quantify the relevance of the top returned results.
4. 🔷 Normalized Discounted Cumulative Gain (nDCG) is like MAP, but weights the relevance of the result by its position.
5. Long and short clicks — Allow to quantify how useful the results are to the real users.
6. A good detailed overview.

🔷 **Human evaluations:** Quality metrics might seem like statistical calculations, but they can’t all be done by automated calculations. Ultimately, metrics need to represent subjective human evaluation, and this is where a “human in the loop” comes into play.
❗️==Skipping human evaluation is probably the most spread reason of sub-par search experiences.==

Usually, at early stages the developers themselves evaluate the results manually. At later point human raters (or assessors) may get involved. Raters typically use custom tools to look at returned search results and provide feedback on the quality of the results.

Subsequently, you can use the feedback signals to guide development, help make launch decisions or even feed them back into the index selection, retrieval or ranking systems.

Here is the list of some other types of human-driven evaluation, that can be done on a search system:

1. Basic user evaluation: The user ranks their satisfaction with the whole experience

2. Comparative evaluation: Compare with other search results (compare with search results from earlier versions of the system or competitors)
3. Retrieval evaluation: The query analysis and retrieval quality is often evaluated using manually constructed query-document sets. A user is shown a query and the list of the retrieved documents. She can then mark all the documents that are relevant to the query, and the ones that are not. The resulting pairs of (query, [relevant docs]) are called a “golden set”. Golden sets are remarkably useful. For one, an engineer can set up automatic retrieval regression tests using those sets. The selection signal from golden sets can also be fed back as ground truth to term re-weighting and other query re-writing models.
4. Ranking evaluation: Raters are presented with a query and two documents side-by-side. The rater must choose the document that fits the query better. This creates a partial ordering on the documents for a given query. That ordering can be later be compared to the output of the ranking system. The usual ranking quality measures used are MAP and nDCG.

**Evaluation datasets:**
One should start thinking about the datasets used for evaluation (like “golden sets” mentioned above) early in the search experience design process. How you collect and update them? How you push them to the production eval pipeline? Is there a built-in bias?

**Live experiments:**
After your search engine catches on and gains enough users, you might want to start conducting live search experiments on a portion of your traffic. The basic idea is to turn some optimization on for a group of people, and then compare the outcome with that of a “control” group — a similar sample of your users that did not have the experiment feature on for them. How you would measure the outcome is, once again, very product specific: it could be clicks on results, clicks on ads etc.

**Evaluation cycle time:** How fast you improve your search quality is directly related to how fast you can complete the above cycle of measurement and improvement. It is essential from the beginning to ask yourself, “how fast can we measure and improve our performance?”

Will it take days, hours, minutes or seconds to make changes and see if they improve quality? ❗️Running evaluation should also be as easy as possible for the engineers and should not take too much hands-on time.
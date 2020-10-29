# common-crawl
## Extract pages related to COVID-19's economic impact using Common Crawl's archives
##### Extracted urls and months can be found in csv ``URLS.csv`` with headers ``url,month``.

### My process
#### 1. Get familiar with Common Crawl
First, I looked over the code example that showed how to use the Common Crawl archives to search for embedded YouTube links. In general, this code makes sense to me. There's a regular expression that contains the pattern for a YouTube url, you load the "stream" to access the archive, and the archive is parsed using ``warc``'s ``ArchiveIterator``. The contents are checked for the regular expression and the code outputs the number of hits and entries.

#### 2. Reading the WARC files
Although the Common Crawl includes a few different file types (WARC/WET/WAT), WARC seems most informative and useful for our purposes. First, I attempted to read in the January 2020 WARC file from the Common Crawl's database. This is where I started facing major difficulties with reading the WARC files. I decided to investigate the different libraries that read WARC files, and the two most well-documented ones I found were ``warc`` and ``warcio``. I attempted to use ``warcio`` first, since that was the one shown in the code example. However, I could not figure out how to read the ``warc.paths.gz`` file from the Common Crawl website, since I kept receiving errors about the file headers. 

Next, I tried using the ``warc`` library to read in my WARC files. I faced major difficulties with this library as well, since I kept receiving error messages that said that the ``__builtin__`` module was not imported. After some searches online, I learned that ``__builtin__`` is now called ``builtins``. So, I tried to change the name of the library inside the warc module itself, which I cloned from GitHub. Unfortunately, there turned out to be several other library errors, and I was not able to import an edited version of the module into my Jupyter Lab.

I spent 2-3 hours looking for libraries that handle WARC files and unsuccessfully testing work-around solutions for the problems I was facing with the ``warc`` and ``warcio`` libraries. The main issue (I believe), either involves a problem with my own dependencies, or with unresolved issues in the ``warc`` and ``warcio`` libraries due to updates in dependent modules. My disastrous attempt at reading WARC files can be found in the ``failed-attempt-at-Common-Crawl`` folder.

#### 3. Assessing non-WARC options
I figured that it was better to find some URLs rather than none, given the challenges I was having with the WARC files. I began looking around at different news companies and seeing if they offered developer APIs to access their article archives. I believed this would be a representative sample of the URL's I would find in the Common Crawl, since news articles most likely make up a significant portion of the Common Crawl pages that contain mentions of COVID and the economy. I chose to start with the NYTimes, since they are a reputable newspaper with a high output volume of articles. (Note: In the end, I did not use the ``news-please`` library, because I I could find all of the relevant information inside the NYTimes API.)

I used a subsection of the NYTimes archives which included all articles from January 1st, 2020 to today. Each article contained metadata, including the URL, a portion of the text, headlines, etc. I compiled economy-related keywords (in ``economy_keywords.txt``) and covid-related keywords (in ``covid_keywords.txt``). I ran keyword searches over the text content of each article and created a list of articles which contained at least one keyword from each category. In total, I found 2570 covid/econ articles from the NYTimes. 

I also attempted to use the News API (formerly Google News) to extract articles. My efforts were only half successful because I needed to buy a paid subscription to extract articles before 9/29/20 and could only make 100 requests in 24 hours.

### Conclusion
I believe I could have figured out the WARC file reading on a different computer, because I'm afraid the dependency problems might be specific to my machine. I acknowledge that I should have used the Common Crawl, but I decided to pivot in a different direction (towards a similar goal) once I saw no options left for reading the WARC files. Regardless, I am incredibly enthusiastic about Trust Lab and sincerely hope we can discuss more about whether I'd be a good fit for the team. Thank you! -- Paige 

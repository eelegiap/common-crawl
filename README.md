# common-crawl
## Extract pages related to COVID-19's economic impact using Common Crawl's archives

### My process
1. Get familiar with Common Crawl
First, I looked over the code example that showed how to use the Common Crawl archives to search for embedded YouTube links. In general, this code makes sense to me. There's a regular expression that contains the pattern for a YouTube url, you load the "stream" for the to access the archive, and the archive is parsed using warc's ArchiveIterator. The contents are checked for the regular expression and the code outputs the number of hits and entries.
2. Reading the WARC files
Although the Common Crawl includes a few different file types (WARC/WET/WAT), WARC seems most informative and useful for our purposes. First, I attempted to read in the January 2020 WARC file from the Common Crawl's database. This is where I started facing major difficulties with reading the WARC files. 

I decided to investigate the different libraries that read WARC files, and the two most common ones I found are ``warc`` and ``warcio``.

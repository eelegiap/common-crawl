# common-crawl
## Extract pages related to COVID-19's economic impact using Common Crawl's archives

### My process
1. Get familiar with Common Crawl
First, I looked over the code example that showed how to use the Common Crawl archives to search for embedded YouTube links. In general, this code makes sense to me. There's a regular expression that contains the pattern for a YouTube url, you load the "stream" for the to access the archive, and the archive is parsed using warc's ArchiveIterator. The contents are checked for the regular expression and the code outputs the number of hits and entries.
2. Reading the WARC files
Although the Common Crawl includes a few different file types (WARC/WET/WAT), WARC seems most informative and useful for our purposes. First, I attempted to read in the January 2020 WARC file from the Common Crawl's database. This is where I started facing major difficulties with reading the WARC files. 

I decided to investigate the different libraries that read WARC files, and the two most well-documented ones I found were ``warc`` and ``warcio``. I attempted to use ``warcio`` first, since that was the one shown in the code example. However, I could not figure out how to read the ``warc.paths.gz`` file from the Common Crawl website, since I kept receiving errors about the file headers. Next, I tried using the ``warc`` library to read in my WARC files. I faced major difficulties with this library as well, since I kept receiving error messages that said that the ``__builtin__`` module was not imported. After some searches online, I learned that ``__builtin__`` is now called ``builtins``. So, I tried to change the name of the library inside the warc module itself, which I cloned from GitHub. Unfortunately, there turned out to be several other library errors, and I was not able to import an edited version of the module into my Jupyter Lab.

I spent 2-3 hours looking for libraries that handle WARC files and unsuccessfully testing work-around solutions for the problems I was facing with the ``warc`` and ``warcio`` libraries. The solution (I believe), either involves a problem with my own dependencies, or with unresolved issues in the ``warc`` and ``warcio`` libraries due to updates in dependent modules.

3. Assessing non-WARC options

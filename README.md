# MusicianNetworkAnalysis

This project contains files and notebooks that analyse the network of essentially all musicians on Wikipedia. The accompanying files must be downloaded to ensure the notebooks run successfully.

**A. Musician Network: MusicianNetworkAnalysis.ipynb**

Our dataset is all about music artists and to start creating our network, we needed a list of artist's names. Rather than scraping Wikipedia's long and convoluted categories and lists of musicians, we decided on using Genius database of artists. We took all 18770 names listed on All Artists on Genius.

However, as explained in more details in MusicianNetworkAnalysis Section 2, this list required to be preprocessed, enriched and cleaned. All in all, we ended up with 10191 Wikipedia page names from which we created the complete network.

From this list, we queried each Wikipedia page to retreive its content, using Wikipedia API as done in Week 1 and 4. As node attributes, we decided to extract from each page the artist's birth year and genres (if specified, otherwise 'Unknown') from the Infobox, as well as the length of the page (number of characters). We also extracted all the links to other wikipedia pages and keep them as edges if they link to another artist in the dataset.

**B. Lyrics: LyricAnalysis.ipynb**

We identified all nodes from the GCC that have a degree of >= 90 (aka the total amount of in and out links from their wiki page) and added them to our initial list. We further reviewed the list and determined if the artists have actual lyrics attached to them in Genius. We did this by attempting to download songs from all of the artists using the Genius Lyrics API. During this process we realised some did not have actual lyrics attached to them (such as if they are a DJ, or a singer attached to a band that has lyrics) - so we removed them. We also encountered various name differences between the node names and the artist name that Genius expected, so we needed to keep track of the correct names.
Later on during community detection, we realised that various communities did not have a lot of representation with the above list of high-degree artists. Thus we identified some communities to enrich, including Spanish artists, German bands (that Victor happens to know), Gospel artists, and French rappers, to ensure that at least 10 artists from those communities had songs downloaded (or if the community had only 6, we took all artists!)
We downloaded each artist's top 20 most popular songs using the Genius Lyrics API. The songs are sorted by popularity due to how many views the song lyrics have had on the Genius website. The songs were saved into a single txt file per artist. Finally, we looked through each txt to check if the songs were in English. We removed artists that have met a certain threshold of having non-English tokens (such as Shakira or J Balvin) from sentiment analysis since LabMT and VADER would not be able to analyse their sentiment appropriately. However we will keep the non-English speaking artists txt files for further TC-IDF and wordcloud analysis!

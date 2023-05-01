Download Link: https://assignmentchef.com/product/solved-cecs-529-homework-4
<br>



Develop a disk-based boolean search engine.

I will give you three         les:

<ol>

 <li>IndexWriter: I have written this class for you. Given an existing PositionalInvertedIndex, this class writes three les to disk in order to support a disk-based indexing system:

  <ul>

   <li>bin: contains all the vocabulary terms from the corpus, concatenated into a single ASCIIencoded le.</li>

   <li>bin: contains the postings data for the terms, using the format shown in lecture. For each term, 4 bytes are written for the document frequency of the term, and then a sequence of 4-byte integers follow, one each for the document IDs in the term’s postings list. The IDs are encoded as gaps, not as raw IDs. Positions are not written to disk… yet.</li>

   <li>bin: a table for mapping vocabulary terms to postings byte o sets, as shown in lecture. This le consists of a sequence of pairs of 8-byte integers; the rst value of each pair points to a byte o set in vocab.bin, indicating the location where the string value of the term exists; the second value points to a byte o set in postings.bin containing the postings data for the term.</li>

  </ul></li>

 <li>DiskInvertedIndex: an adaptation of PositionalInvertedIndex to use the set of les created by IndexWriter to return postings lists, rather than an in-memory data structure. Has methods getPostings(String term) (now returns int[] instead of a List structure) and getDictionary(), like the naive index.</li>

 <li>DiskEngine: has the foundations for a command-line user interface to the disk index. Allows the user to select between building an index for a folder and querying an index for a folder. Uses IndexWriter to build an index and DiskInvertedIndex to query an index.</li>

</ol>

You need to do these things in this assignment:

<ol>

 <li>Look through the code and make sure you understand what is going on. Start with IndexWriter, then DiskInvertedIndex, then DiskEngine. You will need to adapt this system for your second Project milestone.</li>

 <li>Augment IndexWriter so that it also writes term frequencies and positions to disk for each posting. Follow the format from class, using 4 bytes for each value, and writing positions as gaps.</li>

 <li>The method getPostings in DiskInvertedIndex is incomplete. You must nish the method according to the instructions in the comments… otherwise the program won’t work :).</li>

</ol>

Print and turn in ONLY the completed DiskInvertedIndex class.

If you are ambitious, you can try the following additions. These features will need to be incorporated into your next project milestone, so you might as well start now :).

<ol>

 <li>Incorporate positions into the IndexWriter (for each document ID that you write, follow with the number of positions for that document, and then each of the positions in turn) and DiskInvertedIndex (when reading document IDs, you will need to read the number of positions for each document ID, and then seek past 4 bytes × the number of positions).</li>

 <li>Change DiskInvertedIndex.readPostingsFromFile to return an array of DiskPosting objects, where a DiskPosting is a document ID, a term frequency, and an array of integer positions which may be null/empty.</li>

 <li>Add a parameter boolean withPositions to readPostingsFromFile. If that parameter is false, then perform your existing logic: read the term frequency for a posting but don’t actually read the positions. (Why would you sometimes not want to read positions?) If it is true, then read the positions into an array and include that array in your DiskPosting object.</li>

 <li>Add a method getPostingsWithPositions to your DiskInvertedIndex class, that returns a list of DiskPosting objects with their positions, for use with phrase queries.</li>

</ol>

1
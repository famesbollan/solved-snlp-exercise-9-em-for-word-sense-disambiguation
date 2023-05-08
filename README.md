Download Link: https://assignmentchef.com/product/solved-snlp-exercise-9-em-for-word-sense-disambiguation
<br>
In this exercise, you will implement expectation-maximization<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> for word sense disambiguation. You can find the pseudocode on slide 44 of chapter

7.

You will be provided with starter code to help you with the implementation, but you can also write your solution from scratch if you want to. If you are using the starter code, you will have to install the NumPy package on your machine.

<h3>The dataset</h3>

NLTK has a corpus reader for the Senseval 2 dataset. This data set contains data for four ambiguous words: hard, line, serve and interest. You can read more here: http://www.nltk.org/howto/corpus.html (search for ”senseval”). The provided code loads the dataset for you and converts each sample into a sample object. The sample class has two attributes: context and label. Label is the ground truth sense of the ambiguous word. As EM is an unsupervised method, we will only use the labels for final evaluation. Context is the left and right context of the ambiguous word as word IDs: it is a list of integers, which you can use later to index matrices. instances = senseval.instances(hard f)

# All training samples as a list. samples = [sample(inst) for inst in instances]

# Convert contexts to indices so they can be used for indexing. for sample in samples:

sample.context to index(word to id)

Now, ”samples” contains all the sample objects for the ambiguous word ”hard”.

<h3>Implementation</h3>

There are three matrices provided for you, which you will have to use for the implementation: <em>priors</em>, <em>probs </em>and <em>C</em>.

<ul>

 <li><em>priors</em>: It is a vector of length K, where K is the number of clusters. Each value corresponds to a cluster prior <em>p</em>(<em>s<sub>k</sub></em>). It’s initialized randomly.</li>

 <li><em>probs</em>: It is a V x K sized matrix, where V is the size of the vocabulary. Each column is a conditional probability distribution over the words. <em>probs</em>[<em>i,k</em>] is <em>p</em>(<em>v<sub>i</sub></em>|<em>s<sub>k</sub></em>).</li>

 <li><em>C</em>: contains the counts of the words in a given context. The size of the matrix is number of samples x vocabulary size. <em>C</em>[<em>i,j</em>] is <em>C</em>(<em>v<sub>j </sub></em>in <em>c<sub>i</sub></em>), the count of word j in context i.</li>

</ul>

To get a better feel of how to use these matrices read the log  likelihood np(samples, probs, priors): function.

Get the IDs of the words. We will use this to index the rows of the probs matrix:

context index = sample.context words given sense = probs[context.index, :]

This is a matrix: the number of lines is the number of words in the context, the number of columns is number of senses. We multiply this column wise to get the probability of a context given a sense <em>p</em>(<em>c<sub>i</sub></em>|<em>s<sub>k</sub></em>):

context given sense = np.prod(words given sense, axis=0)

This is a vector where each value is a class conditional probability (size is K).

<h3>Exercises</h3>

<ul>

 <li>Briefly describe what EM is and when using it is appropriate? Give an example use case .</li>

 <li>Write the code for the expectation step .</li>

 <li>Write the code for the maximization step. In order to check your implementation, make sure that the log likelihood increases over the iterations .</li>

 <li>The code will print the ordered frequency of the labels within each cluster. Each cluster corresponds to one of the senses of ”hard”. How does the algorithm perform? Briefly explain.</li>

</ul>

Does EM find the global optimum? Explain why/why not?



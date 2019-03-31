## Hidden Markov Model Tagger: HMM-tagger

In this notebook, you'll use the [Pomegranate](https://github.com/jmschrei/pomegranate) library to build a hidden Markov model for part of speech tagging with a [universal tagset](http://www.petrovi.de/data/universal.pdf). Hidden Markov models have been able to achieve >96% tag accuracy with larger tagsets on realistic text corpora. Hidden Markov models have also been used for speech recognition and speech generation, machine translation, gene recognition for bioinformatics, and human gesture recognition for computer vision, and more.

The notebook already contains some code to get you started. You only need to add some new functionality in the areas indicated to complete the project; you will not need to modify the included code beyond what is requested. Sections that begin with **'IMPLEMENTATION'** in the header indicate that you must provide code in the block that follows. Instructions will be provided for each section, and the specifics of the implementation are marked in the code block with a `'TODO'` statement. Please be sure to read the instructions carefully!

## Getting Started

You can choose one of two ways to complete the project. The first method is to use the Workspace embedded in the classroom in the next lesson. The Workspace has already been configured with all the required project files for you to complete the project. Simply open the lesson, complete the sections indicated in the Jupyter notebook, and then click the "submit project" button.

**NOTE:** If you are prompted to select a kernel when you launch a notebook, choose the **Python 3** kernel.

Alternatively, you can download a copy of the project from GitHub [here](https://github.com/udacity/hmm-tagger) and then run a Jupyter server locally with [Anaconda](https://www.anaconda.com/download/).

**NOTES:** These steps are **not** required if you are using the project Workspace.

0. (Optional) The provided code includes a function for drawing the network graph that depends on [GraphViz](http://www.graphviz.org/). You must manually install the GraphViz executable for your OS before the steps below or the drawing function will not work.

1. Open a terminal and clone the project repository:
```
$ git clone https://github.com/udacity/hmm-tagger
```

3. Switch to the project folder and create a conda environment (note: you must already have Anaconda installed):
```
$ cd hmm-tagger
hmm-tagger/ $ conda env create -f hmm-tagger.yaml
```

4. Activate the conda environment, then run the jupyter notebook server. (Note: windows users should run `activate hmm-tagger`)
```
hmm-tagger/ $ source activate hmm-tagger
(hmm-tagger) hmm-tagger/ $ jupyter notebook
```

Depending on your system settings, Jupyter will either open a browser window, or the terminal will print a URL with a security token. If the terminal prints a URL, simply copy the URL and paste it into a browser window to load the Jupyter browser. Once you load the Jupyter browser, select the project notebook (HMM tagger.ipynb) and follow the instructions inside to complete the project.

See below for project submission instructions.

## How to move forward for your code base

- Step 1: Review the provided interface to load and access the text corpus
- Step 2: Build a Most Frequent Class tagger to use as a baseline
- Step 3: Build an HMM Part of Speech tagger and compare to the MFC baseline
- Step 4: (Optional) Improve the HMM tagger

## Useful Links and Tips

- Step 2: **Build a Most Frequent Class tagger**
  - Perhaps the simplest tagger (and a good baseline for tagger performance) is to simply choose the tag most frequently assigned to each word. This "most frequent class" tagger inspects each observed word in the sequence and assigns it the label that was most often assigned to that word in the corpus.
  - how defaultdicts' factory funcion works (https://data-flair.training/blogs/python-defaultdict).
  - how to quickly create objects using namedtuple (https://pymotw.com/2/collections/namedtuple.htm).​
  - get_most_frequent_tags(dict_tags) function returns tag by using the Counter.most_commom(2)[0] 
  
- Step 3: **Build an HMM Tagger**
  
  Emmision Probabilities: Suppose we have 7 different observed unique word from the input sentense. And if we put these unique word to the column table and put the unique tag to the row table then we can count the tag vs word occurence. For example, Mary observed 4 Noun, Jane 2 Noun, Spot 1 Noun then we can calcuate the Emission Probablities on Noun as Mary 4/7, Jane 2/7, and Spot 1/7 etc... so we can express like this; Compute a the emission distribution P(w|t) = C(t,w) / C(t)
  
  Transition Probabilities: Suppose we have observed 3 unique tag from the input sentenses. For example, by using the diagram of HMM, we can observe the transition sequence from <s> to Noun to Modal to Verb and finally <e>. Probably there're several path from <s> to <e> but if we simply put the N M V <e> tags to the column head and put the <s> N M V to the row head then we can calculate the co-occurnece frequency for each cell... such as <s> -> N is 3/4 from different transition paths occurences. So each 
    
  - Add one state per tag
    -The emission distribution at each state should be estimated with the formula:P(w|t)= C(t,w)/C(t)
  - Add an edge from the starting state basic_model.start to each tag
    -The transition probability should be estimated with the formula: P(t|start)=C(start,t)/C(start)
  - Add an edge from each tag to the end state basic_model.end
    -The transition probability should be estimated with the formula:P(end|t)=C(t,end)/C(t)
  - Add an edge between every pair of tags
    -The transition probability should be estimated with the formula:P(t2|t1)=C(t1,t2)/C(t1)


## Evaluation

Your project will be reviewed by a Udacity reviewer against the project rubric [here](https://review.udacity.com/#!/rubrics/1429/view). Review this rubric thoroughly, and self-evaluate your project before submission. All criteria found in the rubric must meet specifications for you to pass. Accuracy of basic model HMM Tagger shows below results;

training accuracy basic hmm model: 97.54%
testing accuracy basic hmm model: 95.95%

## Submission

Once you have completed all of the code implementations, you need to finalize your work by exporting the iPython Notebook as an HTML document. Before exporting the notebook to html, all of the code cells need to have been run so that reviewers can see the final implementation and output. You must then export the notebook by running the last cell in the notebook, or by using the menu above and navigating to File -> Download as -> HTML (.html) Your submissions should include both the html and ipynb files.

Add the "hmm tagger.ipynb" and "hmm tagger.html" files to a zip archive and submit it with the button below. (**NOTE:** If you complete the project in the workspace, then you can submit directly using the "submit" button in the workspace.)
# Word embedding experiments on the WE1S corpus

## Word embeddings for restricted access corpora

*Fabian Offert, Teddy Roland, Devin Cornell, Summer 2018*

- https://we1s.ucsb.edu/research_post/word-embeddings-for-restricted-access-corpora/
- https://github.com/zentralwerkstatt/wcf2vec

Given the problem of a restricted access corpus where full texts cannot be stored locally, a custom implementation of the skip gram algorithm is used to train a word embedding model on as little as a word-context-frequency matrix in a highly memory-efficient way. 

## Word Embeddings for the validation of topic models

*Fabian Offert, Fall 2018*

- https://github.com/zentralwerkstatt/we1s-embed

An embedding of the prototype corpus (20181105_1452_us-newspapers-humanities-250-dedupe) is used to validate the topic models created from the corpus by measuring the density of topic-word clusters in embedding space. The method works and shows that more specific topics create denser clusters, as broader terms appear in more diverse contexts than specific terms.

## Large-scale language model text generation from prototype corpus

*Fabian Offert, Winter 2019*

- https://github.com/zentralwerkstatt/we1s-embed/blob/master/gpt2

The recently published [OpenAI GPT-2 general purpose, large-scale, generative language model](https://openai.com/blog/better-language-models/) is [fine-tuned](https://svilentodorov.xyz/blog/gpt-finetune) on the prototype corpus to see if analysis-by-synthesis would a valuable approach for the WE1S project, similar to the idea described in [this blog post](https://zentralwerkstatt.org/post_latent.html). While the results are not fully transparent -- the GPT-2 model's base corpus/source code has not been made public -- and thus allow no definite conclusions w.r.t. the research questions of the project, they certainly seem to reproduce the general "feel" of the corpus, for instance in its bias towards institutional politics. (Note that the "[.]" sign, which replaces "'s" in the corpus, appears at the correct places, showing that the model is indeed generating text based on the supplied corpus.) Additional samples can be found in the GitHub repo.

Model prompt: **The humanities**

> are the most important professions of our generation, according to this report. The humanities alone account for over a quarter of American university degrees. The teaching and learning of the humanities, in particular, has been a major factor in our understanding of the world today. The humanities are also a critical component of the learning experience on campus, helping students to develop the necessary skills to become effective citizens. Although humanities are not the only fields in which they are important, they account for the highest proportion of undergraduate study in the classroom. The humanities, by their nature, require many hours of study on and off campus. It is important for students to develop skills and understand the human condition. The humanities are essential in creating the capacity to become a citizen. Our study of the humanities also helps us to understand the social and economic changes that have made it possible for the humanities and the American system to survive, thrive, and grow. This report describes the characteristics of American universities and their humanities programs in more detail than any other

Model prompt: **The sciences**

> are much more complex and complex than we know it to be. But the main goal of our effort is to create a technology that could revolutionize our daily lives and put a new focus on science education. Technology is a bridge between science and academia or education, a way of getting the student engaged with his or her understanding of science. It is also a way of building bridges between communities and the sciences. By focusing on the humanities , we may get the next-generation of scientists and engineers back in our classrooms, on the Internet and the new computer programs so that their work becomes more visible and impactful in the world. For instance, one of our programs, a public science education project led by the U_S Geological Survey, will allow students to explore the earth[.] ecosystems and understand its importance to their children, to be part of a network of research programs that will bring discovery and understanding into the nation[.] schools. This is a big step forward for science education. It would be

Model prompt: **The university**

> [.] policy is to make a point of the fact that the university is not being profiled in the same way anymore. The fact is that the average student in higher education in 2014 was only 38 percent white, 27 percent black, and the average student in 2014 was 27 percent Asian. That isn't just a minority population; it[.] also a majority. But the fact is that the statistics are inaccurate. More than half of the students who go to college are being profiled, and a fifth are being misidentified as black and Asian. And yet, while it has been widely acknowledged for more than a decade that the university is being profiled in a similar way -- in race and in demographics -- the university is clearly not being profiled as a school. That[.] why every institution in America has been profiled differently. And the way that the university has been profiled is because it has been -- the problem has been that it has been done so badly by the colleges themselves.

## Future Directions

After running many experiments on the prototype corpus, two problems became apparent: because it is assembled from news sources, the corpus is *too general* to let anomalies appear in the embedding space. In other words, the embedding is *too good* in the sense that it maps general but not corpus-specific relations between words. This is why plain word embeddings will not be very helpful in answering the research questions of the project. Hence, I would like to propose four possible directions that go beyond plain embeddings:

- **Visualizing contributions**: If one recorded the contributions of samples to the different vector space directions during the training process, one could possibly generate samples (maybe using simple Markov chains?)  that maximally activate a single direction. I could see the artificial nature of these generated samples -- likely they would not be coherent -- as a very interesting basis for interpreting the meaning of each vector space direction. See also [this blog post](https://jalammar.github.io/illustrated-word2vec/).

- **Antonym exploration**: It was suggested that antonyms could be an interesting terrain to explore. While antonyms can unfortunately not be inferred from co-occurrence measurements (they appear at the very same spot in a sentence usually), antonyms certainly capture many of the difficulties of operationalizing some of the research questions of the project, as pointed out in [the relevant Ryver thread](https://we1s.ryver.com/#posts/2034247). Potentially interesting approaches could be the integration of a thesaurus into the workflow, similar to the method proposed [here](https://aclweb.org/anthology/N15-1100), or working with hierarchies of potential antonyms, as suggested [here](https://gist.github.com/kylemcdonald/9bedafead69145875b8c).

- **Named entity recognition embedding**: I would be interested in extracting named entities from the corpus and running an embedding just on this data. The hope would be that, similar to an embedding of named entities from Proust's Recherche that I ran once, where character relations were preserved in the embedding space, a meaningful "network" of humanities institutions and people would emerge.

- **Baseline random query corpus vs. targeted corpus**: This one is a bit more involved as it requires the creation of a second corpus. Nevertheless, it would be interesting to compare our query-based corpus to a random-query baseline corpus to identify any corpus-specific relations that might be preserved in the embedding space.
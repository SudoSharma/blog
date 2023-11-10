---
title: "Tinkering with Tensors and Other Great Adventures"
cover:
  image: "images/river.webp"
  alt: "Source: www.pexels.com"
  caption: "Source: www.pexels.com"
  relative: false
date: 2019-03-25
tags: ["Deep Learning", "Research"]
showtoc: true
---

<!-- {{< figure src="images/river.webp" caption="Source: www.pexels.com" >}} -->

On a generally unremarkable Wednesday at the end of 2018, I followed the sagely advice of the internet and embarked on a harrowing journey to the center of Artificial Intelligence; I began implementing a deep learning research paper in Natural Language Processing (NLP).

After many days of taming monsters, hunting down the stuff of which real scientists are made, and staring into the heart of darkness, I emerged [weary, but triumphant](https://github.com/SudoSharma/bimpm_implementation). What follows is an account of the motivations and expectations of tackling a project like this.

Join me if you too dare to venture into the deep (pun intended).

> ...as Ilya likes to say, you need to be prepared to suffer: expect hours of debugging models that refuse to learn, many passes restructuring your code, and building up your own conventions for changing various hyperparameters. But each time you suffer, know that you've built a little bit of skill that will be invaluable for the future.
>
> --- Greg Brockman, [Quora 05/16](https://www.quora.com/What-are-the-best-ways-to-pick-up-Deep-Learning-skills-as-an-engineer)

---

## Motivations

Why implement a research paper? And why NLP?

Let's start with the latter.

Assuming you want to create [beneficial AI for the sustained good of humanity](https://futureoflife.org/ai-principles/) (and I mean, who wouldn't?), you'd necessarily have to create a system capable of advanced reasoning, and which could preferably explain the contents of its consciousness to a human being. Natural Language Understanding (NLU) is a subfield of AI which deals with these fundamental issues, and is itself nested within the larger discipline of NLP.

Stated more simply, **_teaching a machine to understand language is crucial to safely unlocking the mysteries of intelligence itself._**

Additionally, if you followed along with the [flurry](https://arxiv.org/abs/1802.05365) [of](https://arxiv.org/abs/1801.06146) [papers](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf) [released](https://arxiv.org/abs/1810.04805) in 2018, you know that while computer vision has long held the public's attention with its breakthroughs and applications in deep learning, [the age of NLP has arrived](http://ruder.io/nlp-imagenet/). This, and my role as a machine learning engineer for a [conversational AI startup](https://www.avaamo.ai/) in Silicon Valley, significantly motivates my interest in this field.

So, here are two compelling reasons to try and implement a research paper:

1.  **To enhance your understanding.** You simply cannot get a good intuition for how theory works in practice without getting your hands dirty, and *implementing a paper results in very dirty hands.* If you've been teaching yourself topics in deep learning [using](http://neuralnetworksanddeeplearning.com/) [books](https://www.deeplearningbook.org/), [online](https://course.fast.ai/) [courses](https://www.deeplearning.ai/), [and](https://deeplearning.mit.edu/) [recorded](https://www.youtube.com/playlist?list=PLC1qU-LWwrF64f4QKQT-Vg5Wr4qEE1Zxk) [lectures](https://www.youtube.com/playlist?list=PL3FW7Lu3i5Jsnh1rnUwq_TcylNr7EkRe6), this is an essential [next step](https://www.quora.com/How-can-beginners-in-machine-learning-who-have-finished-their-MOOCs-in-machine-learning-and-deep-learning-take-it-to-the-next-level-and-get-to-the-point-of-being-able-to-read-research-papers-productively-contribute-in-an-industry) which unforgivingly exposes any gaps in your knowledge.
2.  **To become a badass.** Replicating the performance of a paper is nontrivial and will test the limits of your engineering ability, as well as your perseverance. Whether you've been at it for a while, or you've just begun in this field, eventually completing a project like this can serve as your "coming of age" ceremony. *It will mark your transition from passive observer to active participant in the AI research community.* You will also develop a store of humility and confidence, which you can then ration for more challenging projects in the future.

If any of this sounds even remotely interesting, then you're in the right place. Roll up those sleeves, slap on some sunscreen, and let's hit the road.

{{< figure src="https://miro.medium.com/v2/resize:fit:1120/1*9g8IzCb2upibzR3vJKzYjQ.jpeg" caption="Let's hit the road! Source: www.pexels.com" >}}

But first, as with any adventure of this nature, we'll want to make sure we are aware of any dangers that lie ahead...

## Expectations

Your experience of replicating a research paper will be influenced by how successful you are in achieving your personal goals. Consequently, the most important thing to remember as you start your journey is to set reasonable expectations for yourself, and of course, to stay hydrated.

### Expectation #1: Research vs. Engineering

Even after reading the [experience of others](http://amid.fish/reproducing-deep-rl), I was still surprised to find that implementing a paper disproportionately teaches you more about engineering than research.

Many online courses will create beautiful environments in which you can play around with deep learning concepts. These can run the gamut from cloud instances with pre-loaded libraries, to fully integrated playgrounds in the browser (think [fast.ai](https://course.fast.ai/) vs. [Udacity](https://www.udacity.com/course/deep-learning-nanodegree--nd101)). This is necessary to lower the barrier of entry for newcomers, allowing them to bask in the full glory of AI early in their careers.

{{< figure src="https://miro.medium.com/v2/resize:fit:1120/1*8ph-NIhUQvB7MHWk-uA9aA.jpeg" caption="There are many details safely hidden in online AI courses. Source: www.pexels.com" >}}

Unfortunately, much like the children of over-protective, but well-intentioned parents, this coddling makes little Johnny unprepared for the real world. It's up to us young'uns to fill in the gaps with practical knowledge.

Here's what I mean:

**_Not only did I grossly underestimate the overall time this project would take, but I also miscalculated the distribution of effort._** I initially assumed I'd knock out the implementation over the weekend, and spend about five days testing out different hypotheses, with a 20/80 split of my time.

In reality, roughly 40% of my time was spent fussing about with operational overhead, 40% with implementing, debugging, and testing the model architecture, and a final 20% with experimentation.

Spread out over a two and a half week period, coding before and after work, and on the weekends, this project took me about 60 hours in total. I spent an additional 20 hours wrestling with model deployment, but more on that later.

For your first paper implementation, this distribution and time commitment profile is not unreasonable, assuming you've chosen a somewhat challenging paper in a discipline with which you have a measure of familiarity.

In general:

1.  **Budget more time than you think you'll need for operational setup, especially for your first paper.** Use this as an opportunity to improve your software engineering skills as well as your problem solving capacity.
2.  **During the implementation phase, constantly run dummy data through your network at appropriate checkpoints.** Convince yourself the output makes sense, and fix it if it doesn't. Definitely don't wait till everything is built to start debugging.
3.  **In order to keep a track of your experiments, as well as to trace an issue back through time, take meticulous notes.** A happy side effect of this is the ability to fondly look back on all you've achieved.

In short, plan well, smell the roses, and take lots of pictures.

### Expectation #2: Reproducibility

The [replication crisis](https://en.wikipedia.org/wiki/Replication_crisis) is a disease that often afflicts the social and medical sciences because of the risky business of doing human subject research. *When academics are unable to reproduce the results of their peers, the engine of scientific discovery itself can grind to a halt.*

You can't very well stand on the shoulders of giants if they're slouching.

This can happen for a number of reasons, including limp research standards, "publish or perish" incentives, and in the limit, downright fraudulent activity. Even when good science is conducted with the best of intentions, it isn't always smooth sailing. In artificial intelligence research, this often takes the form of algorithmic papers with under documented code (if published at all), and whose performance can fluctuate with sensitive training conditions.

What this means for you, intrepid traveller, is that you must not be discouraged if your results don't look EXACTLY like those of your chosen paper's. I discovered rather quickly that *authors will often leave out details because they aren't important (they are) or because they're incredibly obvious (they are not).*

{{< figure src="https://miro.medium.com/v2/resize:fit:1120/1*V03BPsK8TzyqcZtrYIiTYw.jpeg" caption="Authors can leave out seemingly unimportant, but crucial, details. Source: www.pexels.com" >}}

In order to overcome this, you simply cannot limit your study of a research paper to the source text alone. You'll have to marshal external resources (GitHub, StackOverflow, your neighbor), and develop a good intuition for critical concepts which influence every paper, but aren't always made explicit. This will help you intelligently fill in the gaps to ultimately replicate, and hopefully even surpass the performance of deep learning algorithms.

Here are the most common questions authors leave unanswered, but which you'll have to grapple with nonetheless:

#### How were the weights initialized?

In any given layer, you don't want your weights to be the same, too big, or too small. If all the weights were identical to one another, your updates (learning rate times derivative w.r.t each weight) would have the same direction and magnitude.

No bueno.

*Different "neurons" need to change differently in order for your network to learn complex relationships between inputs and outputs* --- this is known as "[breaking symmetry](https://stackoverflow.com/questions/20027598/why-should-weights-of-neural-networks-be-initialized-to-random-numbers)" and is the reason a single layer neural network has the potential to [approximate any continuous function](https://en.wikipedia.org/wiki/Universal_approximation_theorem). In essence, this is why [deep learning is so useful](http://neuralnetworksanddeeplearning.com/chap4.html).

Too big or too small values for your weights will result in [exploding/vanishing gradients](http://neuralnetworksanddeeplearning.com/chap5.html), which ultimately make the training process unstable, slow, or altogether ineffective. If you're driving on the highway, with large gradients you would be hurtling along at 120 mph, and with small gradients, you'd be inching forward at an excruciating 5 mph.

You'll either miss your exit, or die of boredom...and in both cases, you're getting a ticket.

So, in order to have the perfect weights, we'd have make sure they were sampled from [a suitable probability distribution](https://medium.com/usf-msds/deep-learning-best-practices-1-weight-initialization-14e5c0295b94). Because of how important this particular insight is, a lot of really smart people have written entire dissertations on this topic. As a result, *current best practice is to use either He or Xavier initialization for ReLUs (rectified linear units) or tanh/sigmoid activation functions, respectively.*

Unfortunately, these initialization schemes are inherently stochastic, since weights are randomly selected from a distribution. This means that even though neural networks can be deterministic with fixed initial weights and inputs, the replication of a paper becomes NON-deterministic. Your weights, and subsequently your results, will be slightly different, and for now, we'll have to live with that.

{{< figure src="https://miro.medium.com/v2/resize:fit:1120/1*3q3zQQudU3p6T5BFQPqQtQ.jpeg" caption="Initializations can be robust, but ultimately stochastic. Source: www.pexels.com" >}}

Using the above intuition however, you'll at least know not to blame the weights if your results are radically different from that of the paper's. You also won't be stranded if the authors fail to mention any initialization procedures.

#### Which hyperparameters were used?

There are quite a few hyperparameters which play an integral role in bringing a deep learning algorithm to life, the vast majority of which you'll have no trouble discovering.

Descriptions of the size and number of hidden layers, regularization coefficients, and other architectural landmarks are seamlessly intertwined with a compelling discussion of theoretical underpinnings in most research papers.

These *design* hyperparameters give you the blueprints for a successful implementation, but will take you no further. In order to match the performance of the paper, you'll have to hunt for a different species of *training *hyperparameters.

This is where you'll start to sweat.

Where are the learning rates? The batch sizes, the epochs? Moving beyond traditional hyperparameters, what optimizer was used? What was the training and test split in the dataset?

To those satisfied with merely keeping up with recent advances in the artificial intelligence world, these details are insignificant. "I'll just read the paper and move on!" they'll say, "Better yet, is there an abstract I can take a look at?"

But to the grizzled few that want to chase the madness and bend reality to our will, these features are crucial. *Your goal is not simply to understand these papers, but to re-imagine them all together, and perhaps even build on their successes.*

One approach is to scrounge for these training hyperparameters on the internet. You could find a related implementation on GitHub and pluck out relevant values. Unfortunately, wading through internet code can be extremely frustrating and misleading.

A better strategy is to start with first principles, identify best practices, and hone your intuition for these recurring themes:

**Batch Size:** Start with [around 32](https://arxiv.org/abs/1804.07612). Using fewer training examples to update your weights generates a "noisy" gradient signal. Counterintuitively, this noise exerts a [regularizing effect](https://arxiv.org/abs/1609.04836) on your network, allowing it to generalize well to unseen test data.

{{< figure src="https://miro.medium.com/v2/resize:fit:1120/1*Ov3sK36PA6-hMiT0Laz14A.png" caption="Source: [www.twitter.com](https://twitter.com/ylecun/status/989610208497360896)" >}}

**Number of Epochs:** This one is easy. Start with a sufficiently large number of epochs (a full pass through your data) and stop training when the validation error starts to get worse. Assuming you've been saving your weights at regular intervals, pick the ones that give you the lowest validation loss --- this is known as [early stopping](https://machinelearningmastery.com/early-stopping-to-avoid-overtraining-neural-network-models/).

**Training/Validation/Test Sets:** A good rule-of-thumb is to split your dataset 80/10/10. The fewer data points you have however, the more of them you'll push into training, so this ratio can be fluid. Being paranoid about [how data are distributed in these different sets](https://www.fast.ai/2017/11/13/validation-sets/) is not a bad idea, but if your paper is using a well-known benchmark, the details will most likely have been [handled for you in advance](https://www.analyticsvidhya.com/blog/2018/03/comprehensive-collection-deep-learning-datasets/).

**Optimizer:** Go with [AdamW](https://arxiv.org/pdf/1711.05101.pdf), [a better variant of Adam](https://www.fast.ai/2018/07/02/adam-weight-decay/). The basic principle is to choose an optimizer which updates individual parameters according to their "needs", using some fraction of the gradient signal. Think socialism. AdamW combines this adaptive update with momentum, a moving average of previous gradients. This intelligently shifts parameters, while protecting against wild fluctuations in the loss from the current batch.

**Learning Rate:** This is a coefficient that optimizers multiply with the gradient to dampen the error signal (adaptively in AdamW's case). First, use any [learning rate (lr) finder](https://docs.fast.ai/basic_train.html#lr_find) to get a max and min value. Then use a [1cycle policy](https://www.fast.ai/2018/04/30/dawnbench-fastai/) to modulate both your learning rate and your momentum. The intuition here is that network will [rapidly explore solutions](https://arxiv.org/abs/1708.07120) in the beginning, before slowly converging on the optimal parameters.

Reproducibility is incredibly important to scientific progress, so it's a shame when artificial intelligence researchers make it harder for others to follow in their footsteps. Mastering these above concepts will give you the confidence to push forward, even if your paper's authors aren't explicit about training procedures.

What's more, instead of just reading a paper and thinking, "that makes sense", you'll notice a shift in perspective towards, "I agree with this" or "I would've done this differently". Implementing a research paper will evolve from a purely educational activity into an exercise in peer review.

{{< figure src="https://miro.medium.com/v2/resize:fit:1120/1*rLU5w674qyGYVI1WE052hQ.jpeg" caption="Welcome to the scientific enterprise! Source: www.pexels.com" >}}

### Expectation #3: Personal Comforts

While this will undoubtedly be an interesting experience, there are a few things you can do to make sure things go smoothly on your first implementation adventure.

1.  **Select a paper for which the training time is under 5 hours.** This might help reduce the amount of money you spend on your first implementation (depending on the GPU instance you run). More importantly, a faster feedback loop between subsequent training runs lets you experiment quickly and doesn't destroy your self-esteem if there's a bug.
2.  **Start small, and build up to the full implementation.** Definitely do not try and build out the full architecture of the paper, only to realize you've made some tiny mistake which renders your network untrainable. The way around this is to build in pieces, run a batch of data through the network, and convince yourself things make sense. Tackle simpler problems you've constructed for yourself before moving on.
3.  **Wait to experiment until the original results are close to replicable.** As soon I got things working, I started running mini experiments to poke and prod my network, to ultimately observe its behavior. This isn't necessarily a BAD thing, as it might help you develop intuitions, but those intuitions are not grounded in relation to how your implementation should have been working in the first place. So replicate first, experiment soon after.
4.  **Make sure to pick an intellectually stimulating topic that you know something about, or are willing to explore.** I chose to replicate the results from a paper in NLP, which I find fascinating, and which is relevant for my job. This kept me engaged even when the material was challenging and I was even able to apply what I'd learned to algorithms at work.

## Closing Thoughts

Should you dive in head first and learn on-the-go, or should you learn everything you can *before* attempting to implement a research paper? The answer really depends on why you want to do this, and what you hope to get out of this experience.

Regardless of your strategy, the important thing is to realize is that the answers to your questions are not always going to be in the paper itself, and that a conceptual understanding can help fill-in-the blanks when authors are less than explicit. *Perhaps then, a middling path that equips you with the basics before you embark, gives you the best shot of emerging unscathed.*

Up until this point, I've refrained from referencing my actual implementation, since this discussion is largely about motivations and expectations. However, if you are interested, I implemented the [Bilateral Multi-Perspective Matching](https://arxiv.org/pdf/1702.03814v3.pdf) model from IBM for my first attempt at reproducing a deep learning algorithm. You can find my experiments, code, and tests on [GitHub](https://github.com/SudoSharma/bimpm_implementation). Everything is heavily documented, and I've made things really easy to understand. Happy digging!

There is certainly more that can be said about replicating the performance of a deep learning paper (tools, debugging strategies, measuring experiments, etc.), and perhaps I'll go into some of these in a future article. But for now, hopefully you found this piece instructive in planning your adventure, and understanding some of the surprises (pleasant or otherwise) that await you on your journey.

So then, bold traveller, stay safe but curious, pack light, and remember to take it all in! Bon Voyage!

{{< figure src="https://miro.medium.com/v2/resize:fit:1600/1*uhIFSefDRrOU3keaAvsL1Q.jpeg" caption="Bon Voyage! Source: www.pexels.com" >}}

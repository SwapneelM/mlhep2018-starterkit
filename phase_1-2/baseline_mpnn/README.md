# Solution for the MLHEP 2018 Challenge

- You can find details of the challenge on [CodaLab](https://competitions.codalab.org/competitions/19818)

## Getting Started

- If you just want to quickly get started with the contest, follow these steps:

    - Download the dataset for the current ongoing phase (Phase 3, as of August 16 2018)
    - Extract the hdf5 files containing training and testing data into a directory
    - Provide the path to the directory within the `baseline_mpnn` Notebook
    - Run all Cells

## Tips and Tricks

- The IO is visibly a bottleneck so if you want you can rewrite the file reading/writing using a library of your choice - I had attempted this with [h5py](http://www.h5py.org/) but I didn't have enough time to develop a replacement for the existing function in the `tools/base.py` file named `hdf5_to_numpy`.

- The organisers were quick to follow-through on this and added a CSV-compatible version of the notebook based on the suggestions and code by another participant at the school: https://github.com/mmajewsk

- I was too deep into training my MPNN to consider the switch although it would have saved me time. If you are just starting out, do take a look at my notebook but also check out the file reading/writing to CSV since it saves you about 20 minutes on an average (this is what I heard).

- Finally, the simplest trick to work faster is to avoid re-running the cells that read in the training and testing examples (I have mentioned these as `Custom Blocks` within my notebook. Do take a look in case it helps you shave off quite a bit of time running the model.

## Background for the Competition

- The Organisers were kind enough to provide an almost complete version of the models for us to play around with prior to the start of the competition. Since we had but a few hours each day (after ~10 hours of lectures/tutorials daily), this was a really good idea!

- Understandably, there was little time to tweak around the baseline Message-passing Neural Network Architecture. So in my case, I played around mostly with the Learning Rate and Number of Epochs for Training.

## Breakpoints

- A few noteworthy results included 0.00 accuracy the first few times for the simple reason that I was not reading all the training examples and corresponding to this the code does not write out a file with 10,000 entries. Thus, the submission is evaluated as incomplete.

- When I did get it to run, though, I figured out a few tweaks and hacks worth mentioning. Note that these are the bare basics of training ML models but since that's what I really stuck to, that's been my approach:

    1. Do not try to read in all the training examples. There are 10,000 of them and the way the current code is structured, they are read line-by-line. You can imagine why they take nearly 30 minutes to read and an hour to write the submission file (forget about the training time).
    2. Try training it in sets of epochs and then looking at the accuracy before moving forward. A few of the times, I realised midway that it was overfitting and was able to avoid the wastage of training time and resources that would yield worse results.

## Approach

- My approach was basically just to train it on a couple hundred epochs while intermittently monitoring the training accuracy and losses.

- I arrived at an ideal (relatively well-performing) combination of parameters for the learning rate and number of epochs, and that was essentially my solution.

- The part worth noting here is that it isn't possible to brute-force the training - more epochs does not imply better accuracy or lower losses.

- The other aspect is also that a sub-optimal learning rate can either be too low or too high: either it converges way too slow, or converges too fast and then keeps bouncing around, never really arriving at the minima.

## Conclusion

- If you'd like to use this solution please feel free to do so. I'm also open to suggestions for where I missed something or incorrectly deduced a conclusion.

- I'd like to thank Yandex, HSE, and Oxford University for a wonderful deep-dive into machine learning for particle physics!

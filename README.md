# Transfer Learning Tutorial

A guide to train the inception-resnet-v2 model in TensorFlow. Visit [here](https://kwotsin.github.io/tech/2017/02/11/transfer-learning.html) for more information.

### Common Issues:

**Q:** Why is my code trying to restore variables like `InceptionResnetV2/Repeat_1/block17_20/Conv2d_1x1/weights/Adam_1` when they are not found in the .ckpt file?

**A:** The code is no longer trying to restore variables from the .ckpt file, but rather, from the log directory where the checkpoint models of your previous training are stored. This error happens when you have changed the code but did not remove the previous log directory, and so the Supervisor will attempt to restore a checkpoint from your previous training, which will result in a mismatch of variables. 

**Solution: Simply remove your previous log directory and run the code again.** This applies to both your training file and your evaluation file. See this [issue](https://github.com/kwotsin/transfer_learning_tutorial/issues/2) for more information.

**Q:** Why is my loss performing so poorly after I updated the loss function from `slim.losses.softmax_cross_entropy` to `tf.losses.softmax_cross_entropy`?

**A:** The position of the arguments for the one-hot-labels and the predictions have changed, resulting in the wrong loss computed. This happens if you're using an older version of the repo, but I have since updated the losses to `tf.losses` and accounted for the change in argument positions.

**Solution: `git pull` the master branch of the repository to get the updates.**

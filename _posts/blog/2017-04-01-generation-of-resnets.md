---
layout: post
title: "Generation of Residuals"
categories: blog
date: 2017-04-01
---

Deep Learning has already transformed computing industry. Video, image, content, speech and language analysis and many others topics has already changed. Today, the buzzword _Deep Learning_ mostly associated with _Convolutional_ and _Recurrent_ neural networks. To be honest, there are huge amount of work around other stuff such like Adversarial Neural Networks, Bayesian Neural Networks, Mixtures of Convolutions and Recurrent nets. I was being torn to pieces by deciding what to write about first. I decided to start from the culprip of Deep Learning success - the CNNs, by the way this is not an American TV channel, and its derivatives residual networks which hold all the aces in some tasks.

Learning of deep neural networks is very time consuming. Even more powerful GPUs does not guarantee fast convergence of neural networks.

It can be a distraction that very deep neural networks are much more efficient than shallower, but taller. By taller I mean higher number of activation units per layer.

The residual conception made  become the researches hunt for convolutional
architectures which are deeper.

Since [LeNet-5](), we can observe that depth of neural networks increases drastically. Extensive number of optimization, regularization and architecture specific approaches has been invented to make indeed deep nets possible. I have to give a credit for some these methods, which are building bricks in deep learning now:

* [_Stochastic Gradient Decent_]() and all its advanced descendants: Adam, SGD with momentum, Adagrad, RMProp. In fact, it is important to mention that I mean SGD with [mini-batches]().
* [_Rectified linear unit_]() activation function and its modifications: leaky ReLU, ELU, Parameterized ReLU. ReLU is just \\( max(0, x) \\) and has TODO
* Well known by standard machine learning [_Weight Decay_]() technique, noted also as L2-regularization. This is an artificial constraint term \\( \frac{\lambda}{2}\sum_{}w^2 \\), the sum of squared weight parameters \\(w\\) with regularization factor \\(\lambda\\), which is injected or added to loss function to prevent overfitting and improve generalization of the model.
* [_Dropout_]() layers. Another one regularization method
* [_Batch Normalization_]()

You have so many ways for optimization in your machine learning toolbox and you can build convolutional nets with hundreds of layers. Even though with these available procedures, we can not build truly deep networks. You will get stuck either with training for days or non converging model at all.

One of the deepest neural architectures where were used some of these approaches is [VGG](https://arxiv.org/pdf/1409.1556) with 16 and 19 layers and it has tremendous number of parameters, more than `100` millions. The [analysis of deep nets for practical applications](https://arxiv.org/pdf/1605.07678) shows VGG does not utilize well its parametric space.

If you want to go beyond of tens of layers then you must be aware of another one trick. It is known as residual, skip or shortcut connections. This architecture's technique was introduced in by Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun in [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385), I am compelled to mention about [Highway Network](https://arxiv.org/abs/1505.00387) paper of Rupesh Kumar Srivastava, Klaus Greff, Jürgen Schmidhuber because they did discover it first or in the same time, they just moved their research in a different direction. Also, I have to include to contibutor's list the [GoogleNet](http://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Szegedy_Going_Deeper_With_2015_CVPR_paper.pdf) paper - the residual connection is less pronounced in their work.

The imperfection is in the nature of backpropogation of the gradients. Yes, this algorithm is main success precodition of the neural networks and meanwhile it is one of the biggest headaches in learning process of them. The  backpropogation nature lies in broadcasting an error or derivatives from loss function to relative layer's parameters. Indeed, it is wise implementation of [chain rule](https://en.wikipedia.org/wiki/Chain_rule) of partial derivatives, which looks as \\( \frac{df_{3}(f_{2}(f_{1}(x)))}{dx} = \frac{df_{3}}{df_{2}}\frac{df_{2}}{df_{1}}\frac{df_{1}}{dx} \\), where \\(f_{3}\\) is loss function and \\(\frac{df_{3}}{df_{2}} = \frac{df_{3}}{dw_{2,3}}\\), \\(\frac{df_{3}}{df_{1}} = \frac{df_{3}}{dw_{1,2}}\\) and \\(\frac{df_{3}}{df_{1}} = \frac{df_{3}}{dw_{0,1}}\\). According to gradient decent you must update layer's parameters following the [delta rule](https://en.wikipedia.org/wiki/Delta_rule). For example the revise process of first layer parameters should look like \\( w_{0,1} = w_{0,1} - \alpha \frac{df_{3}}{dw_{0,1}} \\), where \\(\alpha\\) is learning rate. That is pretty simple, isn't it? But, unfortunately, the simplicity in this case does not mean lack of shortcomings. The multiplicative form of an operation for obtaining the gradient is a root of problem. Look at \\( \frac{df_{3}}{df_{1}} = \frac{df_{3}}{df_{2}}\frac{df_{2}}{df_{1}}\\), if one of the gradients \\( \frac{df_{3}}{df_{2}}\\), \\(\frac{df_{2}}{df_{1}}\\) in the chain is much less or much greater than \\(1.0\\), near to \\(0.0\\) or \\(\pm\infty\\), then it causes update process of _all_ leading layer parameters harmfully. This trouble acclaimed as _vanishing and exploding gradient_.

The next serious obstacle for having indeed convolutional deep nets is _diminishing problem_. It is less famous as _vanishing and exploding gradient_ problem, but still it is essential for understanding why residual connections may work. This matter refers to forward propogation step.

\\[ h(x) = f(x, w) + g(x) \\]

where, the \\( f(x, w) \\) is a layer or a block of convolutional layers with \\( w \\)
paramters, but your imagination should not be constraint by this cliche; the \\( g(x) \\)
is

\\[ h^{l}(h^{l-1}(x)) = F(H^{l-1}(x)) + G(H^{l-1}(x)) \\]


According to _universal approximation theorem_ the single layer neural network can
represent any function.

There is inge work which

The most disappointing fact is that there are no rigid mathematical proofs of
neural network

Efficiency of extracting better structure of input data advances with depth of the network.

inter-block activations

```yaml
markdown: kramdown
mathjax: true
```

Here is an example MathJax inline rendering \\( 1/x^{2} \\), and here is a block rendering:
\\[ \frac{1}{n^{2}} \\]

\\[ \sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6} \\]

The Power of Depth for Feedforward Neural Networks: https://arxiv.org/pdf/1512.03965v4.pdf, expressive power of neural networks of bounded size
We show that there is a simple (approximately radial) function on R
d, expressible by a small 3-layer
feedforward neural networks, which cannot be approximated by any 2-layer network, to more than a
certain constant accuracy, unless its width is exponential in the dimension. The result holds for virtually
all known activation functions, including rectified linear units, sigmoids and thresholds, and formally
demonstrates that depth – even if increased by 1 – can be exponentially more valuable than width for
standard feedforward neural networks. Moreover, compared to related results in the context of Boolean
functions, our result requires fewer assumptions, and the proof techniques and construction are very
different

Do Deep Nets Really Need to be Deep? https://arxiv.org/pdf/1312.6184.pdf
Intro: Currently, deep neural networks are the state of the art on problems such as speech
recognition and computer vision. In this paper we empirically demonstrate that
shallow feed-forward nets can learn the complex functions previously learned by
deep nets and achieve accuracies previously only achievable with deep models.
Moreover, in some cases the shallow nets can learn these deep functions using the
same number of parameters as the original deep models. On the TIMIT phoneme
recognition and CIFAR-10 image recognition tasks, shallow nets can be trained
that perform similarly to complex, well-engineered, deeper convolutional models.
Conclution: We demonstrate empirically that shallow neural nets can be trained to achieve performances previously
achievable only by deep models on the TIMIT phoneme recognition and CIFAR-10 image
recognition tasks. Single-layer fully connected feedforward nets trained to mimic deep models can
perform similarly to well-engineered complex deep convolutional architectures. The results suggest
that the strength of deep learning may arise in part from a good match between deep architectures
and current training procedures, and that it may be possible to devise better learning algorithms to
train more accurate shallow feed-forward nets. For a given number of parameters, depth may make
learning easier, but may not always be essential.

DO DEEP CONVOLUTIONAL NETS REALLY NEED TO
BE DEEP AND CONVOLUTIONAL? https://arxiv.org/pdf/1603.05691.pdf


Deep vs. Shallow Networks: an Approximation Theory Perspective
The paper briefly reviews several recent results on hierarchical architectures for learning from
examples, that may formally explain the conditions under which Deep Convolutional Neural Networks perform much
better in function approximation problems than shallow, one-hidden layer architectures. The paper announces new
results for a non-smooth activation function – the ReLU function – used in present-day neural networks, as well as
for the Gaussian networks. We propose a new definition of relative dimension to encapsulate different notions of
sparsity of a function class that can possibly be exploited by deep networks but not by shallow ones to drastically
reduce the complexity required for approximation and learning.
https://arxiv.org/pdf/1608.03287.pdf

Going deeper with convolutions 22 layers 2014 year: https://arxiv.org/pdf/1409.4842.pdf
George Cybenko. Approximation by superpositions of a sigmoidal function. Mathematics of Control, Signals
and Systems, 2(4):303–314, 1989.
Gross, S., Wilber, M.: Training and investigating residual nets (2016)
http://torch.ch/blog/2016/02/04/resnets.html

DEMYSTIFYING RESNET https://openreview.net/pdf?id=SJAr0QFxe


Following update rule of gradient decent TODO it means that if you want to find derivatives of loss function with respect to the layer which parameters you are going to update. Let's say that \\(x\\) is an input image, \\(f_{3}\\) is a loss function and \\(f_{1}, f_{2}\\) are hidden layers with \\(w_{1}, w_{2}\\) parameters. our derivatives or delta errors in multiplicative manner. It means that when ever we have derivatives on backprop way less than 0, the gradients of first

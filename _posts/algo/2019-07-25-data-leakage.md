---
layout: post
title:  Data Leakage
date:   2019-07-25 12:00:00
category: "algo"
keywords: data leakage
---

Data Leakage是机器学习任务中很常见的一种错误，看几个类似定义

比如

> According to Kaggle, data leakage is the creation of unexpected additional information in the training data, allowing a model to make unrealistically good predictions. Or a simpler definition, anything that will make your model perform better in research than in production. 

再比如

> If any other feature whose value would not actually be available in practice at the time you’d want to use the model to make a prediction, is a feature that can introduce leakage to your model.

再比如

> When the data you are using to train a machine learning algorithm happens to have the information you are trying to predict.

简单讲，就是模型利用了与label相关的信息，但真实预测场景下，这些信息并不能获得。

导致Data Leakage常见错误

+ bug in the model (like entering the label as a feature)
+ bug in dataset creation (like creating a feature that contains information about the future)
+ bug in the business logic (like using features that cannot be used in production)

典型表现比如离线评估指标很好，线上指标被吊打。

Refs

+ [Data Leakage in Machine Learning](https://machinelearningmastery.com/data-leakage-machine-learning/)
+ [Data Leakage](https://www.kaggle.com/dansbecker/data-leakage)
+ [Top Examples of Why Data Science is Not Just .fit().predict()](https://towardsdatascience.com/top-examples-of-why-data-science-is-not-just-fit-predict-ce7a13ef7663)





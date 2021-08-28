# hw1

```python
import sys
if sys.version_info[0] < 3:
    raise Exception("Python 3 not detected.")
import numpy as np
import matplotlib.pyplot as plt
from sklearn import svm
from scipy import io
from scipy.io import loadmat
for data_name in ["mnist", "spam", "cifar10"]:
    data = io.loadmat("data/%s_data.mat" % data_name)
    print("\nloaded %s data!" % data_name)
    fields = "test_data", "training_data", "training_labels"
    for field in fields:
        print(field, data[field].shape)

mnist_data = io.loadmat("data/mnist_data.mat")
spam_data = io.loadmat("data/spam_data.mat")
cifar10_data = io.loadmat("data/cifar10_data.mat")

from sklearn.model_selection import train_test_split
mnistX_train, mnistX_val, mnistY_train, mnistY_val = train_test_split(
    mnist_data["training_data"], mnist_data["training_labels"], test_size=10000, shuffle=True)

spamX_train, spamX_val, spamY_train, spamY_val = train_test_split(
    spam_data["training_data"], spam_data["training_labels"], test_size=0.2, shuffle=True)

cifar10X_train, cifar10X_val, cifar10Y_train, cifar10Y_val = train_test_split(
    cifar10_data["training_data"], cifar10_data["training_labels"], test_size=5000, shuffle=True)

from sklearn.metrics import accuracy_score
from sklearn import svm

training_sizes = [100, 200 ,500, 1000, 2000, 5000, 10000]
training_acc = []
validation_acc = []
clf = svm.SVC(kernel='linear')
for training_size in training_sizes:
    clf.fit(mnistX_train[:training_size], mnistY_train[:training_size])
    predicted_val = clf.predict(mnistX_val)
    predicted_train = clf.predict(mnistX_train[:training_size])
    validation_acc.append(accuracy_score(mnistY_val, predicted_val))
    training_acc.append(accuracy_score(mnistY_train[:training_size], predicted_train))


x = np.arange(len(training_sizes))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different sizes of training set')
ax.set_xticks(x)
ax.set_xticklabels(training_sizes)
ax.legend()


fig.tight_layout()

plt.show()

training_sizes = [100, 200 ,500, 1000, 2000, 5172]
training_acc1 = []
validation_acc1 = []
clf1 = svm.SVC(kernel='linear')
for training_size in training_sizes:
    clf1.fit(spamX_train[:training_size], spamY_train[:training_size])
    predicted_val = clf1.predict(spamX_val)
    predicted_train = clf1.predict(spamX_train[:training_size])
    validation_acc1.append(accuracy_score(spamY_val, predicted_val))
    training_acc1.append(accuracy_score(spamY_train[:training_size], predicted_train))


x = np.arange(len(training_sizes))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc1, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc1, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different sizes of training set')
ax.set_xticks(x)
ax.set_xticklabels(training_sizes)
ax.legend()


fig.tight_layout()

plt.show()

training_sizes = [100, 200 ,500, 1000, 2000, 5000]
training_acc2 = []
validation_acc2 = []
clf2 = svm.SVC(kernel='linear')
for training_size in training_sizes:
    clf2.fit(cifar10X_train[:training_size], cifar10Y_train[:training_size])
    predicted_val = clf2.predict(cifar10X_val)
    predicted_train = clf2.predict(cifar10X_train[:training_size])
    validation_acc2.append(accuracy_score(cifar10Y_val, predicted_val))
    training_acc2.append(accuracy_score(cifar10Y_train[:training_size], predicted_train))

x = np.arange(len(training_sizes))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc2, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc2, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different sizes of training set')
ax.set_xticks(x)
ax.set_xticklabels(training_sizes)
ax.legend()


fig.tight_layout()

plt.show()

training_sizes = [100, 200 ,500, 1000, 2000, 5000, 10000]

x = np.arange(len(training_sizes))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different sizes of training set')
ax.set_xticks(x)
ax.set_xticklabels(training_sizes)
ax.legend()


fig.tight_layout()

plt.show()

training_sizes = [100, 200 ,500, 1000, 2000, 5172]
x = np.arange(len(training_sizes))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc1, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc1, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different sizes of training set')
ax.set_xticks(x)
ax.set_xticklabels(training_sizes)
ax.legend()


fig.tight_layout()

plt.show()

training_sizes = [100, 200 ,500, 1000, 2000, 5000]
x = np.arange(len(training_sizes))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc2, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc2, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different sizes of training set')
ax.set_xticks(x)
ax.set_xticklabels(training_sizes)
ax.legend()


fig.tight_layout()

plt.show()

paraC = [0.0001, 0.001, 0.01, 0.1, 1, 10, 100, 200]

training_acc = []
validation_acc = []
training_size = 1000
for parameter in paraC:
    clf = svm.SVC(C=parameter, kernel='linear')
    clf.fit(mnistX_train[:training_size], mnistY_train[:training_size])
    predicted_val = clf.predict(mnistX_val)
    predicted_train = clf.predict(mnistX_train[:training_size])
    validation_acc.append(accuracy_score(mnistY_val, predicted_val))
    training_acc.append(accuracy_score(mnistY_train[:training_size], predicted_train))


x = np.arange(len(paraC))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different C')
ax.set_xticks(x)
ax.set_xticklabels(paraC)
ax.legend()


fig.tight_layout()

plt.show()

training_acc1 = []
validation_acc1 = []
training_size = 5000
for parameter in paraC:
    clf1 = svm.SVC(C=parameter, kernel='linear')
    clf1.fit(spamX_train[:training_size], spamY_train[:training_size])
    predicted_val = clf1.predict(spamX_val)
    predicted_train = clf1.predict(spamX_train[:training_size])
    validation_acc1.append(accuracy_score(spamY_val, predicted_val))
    training_acc1.append(accuracy_score(spamY_train[:training_size], predicted_train))


x = np.arange(len(paraC))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc1, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc1, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different C')
ax.set_xticks(x)
ax.set_xticklabels(paraC)
ax.legend()


fig.tight_layout()

plt.show()

training_acc2 = []
validation_acc2 = []
training_size = 1000
for parameter in paraC:
    clf2 = svm.SVC(C=parameter, kernel='linear')
    clf2.fit(cifar10X_train[:training_size], cifar10Y_train[:training_size])
    predicted_val = clf2.predict(cifar10X_val)
    predicted_train = clf2.predict(cifar10X_train[:training_size])
    validation_acc2.append(accuracy_score(cifar10Y_val, predicted_val))
    training_acc2.append(accuracy_score(cifar10Y_train[:training_size], predicted_train))

x = np.arange(len(paraC))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc2, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc2, width, label='Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different C')
ax.set_xticks(x)
ax.set_xticklabels(paraC)
ax.legend()


fig.tight_layout()

plt.show()

from sklearn.utils import shuffle
spamX, spamY = shuffle(spam_data["training_data"], spam_data["training_labels"], random_state=0)
spamX, spamY = spamX[:5000], spamY[:5000]
training_acc1 = []
validation_acc1 = []

for parameter in paraC:
    train_acc = 0
    val_acc = 0
    clf1 = svm.SVC(C=parameter, kernel='linear')
    for i in range(5):
        aX = spamX[0:i*1000]
        bX = spamX[(i+1)*1000:5000]
        aY = spamY[0:i*1000]
        bY = spamY[(i+1)*1000:5000]
        spamX_train, spamY_train = np.concatenate((aX, bX), axis=0), np.concatenate((aY, bY), axis=0)
        spamX_val, spamY_val = spamX[i*1000:(i+1)*1000], spamY[i*1000:(i+1)*1000]

        clf1.fit(spamX_train, spamY_train)
        predicted_val = clf1.predict(spamX_val)
        predicted_train = clf1.predict(spamX_train)
        val_acc += accuracy_score(spamY_val, predicted_val)
        train_acc += accuracy_score(spamY_train, predicted_train)
    validation_acc1.append(val_acc/5)
    training_acc1.append(train_acc/5)


x = np.arange(len(paraC))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, training_acc1, width, label='Training Accuracy')
rects2 = ax.bar(x + width/2, validation_acc1, width, label='Cross-Validation Accuracy')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Accuracy')
ax.set_title('Accuracies on different C')
ax.set_xticks(x)
ax.set_xticklabels(paraC)
ax.legend()


fig.tight_layout()

plt.show()
```

## _\(a\)_

$$\tag{1} \frac{\partial E(3)}{\partial \omega}=2\omega - \sum_{i=1}^{n}\lambda_iy_ix_i$$ $$\tag{2} \frac{\partial E\(3\)}{\partial \alpha} = - \sum\_{i=1}^{n}\lambda\_iy\_i

$$
Let $Eq(1) = 0,\;Eq(2)=0$ we get
$$\tag{3}
\sum_{i=1}^{n}\lambda_iy_i = 0\\
\omega = \frac{1}{2}\sum_{i=1}^{n}\lambda_iy_ix_i
$$

substitute $\(3\)$ into $Eq\(3\)$ to get $Eq\(4\)$.

## _\(b\)_

substitute $\(3\)$ into it.

## _\(c\)_

$\lambda\_i^{_}&gt;0$ means $y\_i\(X\_i\cdot \omega^{_}+\alpha^{\*}\)=1$ All these points' distance to decision boundary is 0.

## _\(d\)_

Consider $Eq\(3\)$ and Q\(c\), not support vectors' $\lambda\_i^{\*}=0$ which means they don't effect $Eq\(3\)$.

## _\(e\)_

**linearly separable:** This data is linearly separable because there is a line \(actually many lines\) from lower left to upper right that separates the red and blue classes.

linearly separable $\iff$ for all points in class $C$, $X\_i\cdot \omega + \alpha &gt; 0 \iff \exist \varepsilon&gt;0 \;s.t. \; X\_i\cdot \omega + \alpha \geq \varepsilon \iff X\_i\cdot \frac{\omega}{\varepsilon} + \frac{\alpha}{\varepsilon} \geq 1$. 昨天理解错了题意，问的是两个类别里都至少有一个点是support vector.

Proof: Consider all $X_i \in C$, if don't exist support vector in this class. $X\_i\cdot \omega + \alpha &gt; 1$. Let $d = \min_{X\_i\in C}X\_i\cdot \omega + \alpha - 1 &gt; 0$. So $X\_i\cdot \omega + \alpha \geq 1 + d \iff X\_i\cdot \frac{\omega}{1+d} + \frac{\alpha}{1+d} \geq 1$. $\|\|w\|\|&gt;\|\|\omega/\(1+d\)\|\|$. For all points $X\_j$ not in $C$, $X\_j\cdot \omega + \alpha \leq 1 &lt; 1+d \iff X\_j\cdot \frac{\omega}{1+d} + \frac{\alpha}{1+d} &lt; 1$. $\frac{\omega}{1+d}$ also satisfies the constrains and its module is less than $\omega$. So $\omega$ is not the solution. The same process of proof is applied for points not in $C$. Thus there is at least one support vector for each class.


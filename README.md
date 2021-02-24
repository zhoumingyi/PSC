# Piecewise Sampling Curving

---
## Usage

#### 1. Demo
<font size=2>Simply run command below, you can get AUC of FGSM, BIM and PGD on MNIST.</font>
```
Python psc.py
```

#### 2. Test
<font size=2>Please put your result (csv file) into the csv/data/YourAdv.csv, then run:</font>
```
Python psc.py --data=MNIST --attack=['FGSM', 'BIM', 'PGD', 'YourAdv'] \
              --d=5 --r=10 --range=[0., 3.] --lines=[129, 252, 502, n]
```
* <font size=2> data: dataset your attack performs on. </font>
* <font size=2> attack: attack methods you want to compare with. </font>
* <font size=2> d: the order of the Polynomial. </font>
* <font size=2> r: resolution of your x-axis. </font>
* <font size=2> range: the range of your x-axis. </font>
* <font size=2> lines: the max line number for attack methods to search in csv. </font>

#### 3. Reproduce
<font size=2>Results on this project can be generated based on settings below.</font>

##### 3.1. Prerequisites
* <font size=2> Python 3.6 </font>
* <font size=2> Pytorch 1.0+ </font>

##### 3.2. Pretrained Model
<font size=2> We used three pretrained models in this project.</font>
* <font size=2> [Net](https://drive.google.com/drive/folders/1cO1lEXiiQgUE9PKdXsuVr5TsPEAS4ras) for MNIST </font>
* <font size=2> [VGG16](https://drive.google.com/drive/folders/1zMUAV4rV0pYIayOCWB4iCIMN0vHOfWUs) for CIFAR-10 </font>
* <font size=2> VGG16 for ImageNet: Pytorch pre-trained model </font>

---
## Benchmarking

We benchmark various adversarial attack methods under PSC (Piecewise Sampling Curving) framework thoroughly on three datasets: MNIST, CIFAR-10 and ImageNet.

#### 1. MNIST
##### 1.1 Gradient-based Attacks (x - attack distance $\ell_2$, y - attack success rate)
<table>
    <tr>
        <td rowspan='2' style="text-align:center">Attack</td>
        <td rowspan='2' style="text-align:center">Model</td>
        <td colspan='2' style="text-align:center">AUC@[0.0, 3.0]</td>
    </tr>
    <tr>
        <td style="text-align:center">Untargeted</td>
        <td style="text-align:center">Targeted</td>
    </tr>
    <tr>
        <td style="text-align:left">FGSM</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">0.26</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">BIM</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">1.37</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">PGD</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">1.48</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">MIA</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
<table>

##### 1.2.1 Score-based Attacks (x - attack distance $\ell_2$, y - attack success rate)
<table>
    <tr>
        <td rowspan='2' style="text-align:center">Attack</td>
        <td rowspan='2' style="text-align:center">Model</td>
        <td colspan='2' style="text-align:center">AUC@[0.0, 3.0]</td>
    </tr>
    <tr>
        <td style="text-align:center">Untargeted</td>
        <td style="text-align:center">Targeted</td>
    </tr>
    <tr>
        <td style="text-align:left">Bandits</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">Square</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">SimBA-DCT</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
<table>

##### 1.2.2 Score-based Attacks (x - number of queries, y - attack success rate)
<table>
    <tr>
        <td rowspan='2' style="text-align:center">Attack</td>
        <td rowspan='2' style="text-align:center">Model</td>
        <td colspan='2' style="text-align:center">AUC@[-, -]</td>
    </tr>
    <tr>
        <td style="text-align:center">Untargeted</td>
        <td style="text-align:center">Targeted</td>
    </tr>
    <tr>
        <td style="text-align:left">Bandits</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">Square</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">SimBA-DCT</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
<table>

##### 1.3. Decision-based Attacks (x - number of queries, y - attack distance $\ell_2$)
<table>
    <tr>
        <td rowspan='2' style="text-align:center">Attack</td>
        <td rowspan='2' style="text-align:center">Model</td>
        <td colspan='2' style="text-align:center">AUC@[-, -]</td>
    </tr>
    <tr>
        <td style="text-align:center">Untargeted</td>
        <td style="text-align:center">Targeted</td>
    </tr>
    <tr>
        <td style="text-align:left">Boundary</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">HSJA</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
    <tr>
        <td style="text-align:left">RayS</td>
        <td style="text-align:center">VGG-16</td>
        <td style="text-align:center">-</td>
        <td style="text-align:center">-</td>
    </tr>
<table>

#### 2. CIFAR-10

#### 3. ImageNet


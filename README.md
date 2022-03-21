# NIH Chest X-ray WebDataset Subset

This dataset is a sample subset of the NIH Chest X-ray Dataset. While its size
of 960 MB is only 2.2% of the size of the original dataset, it still allows
creating an accurate classifier using
[Augmented Chest X-Ray](https://github.com/MichaelNoya/augmented-chest-xray).
The subset is stored in a collection of WebDataset tar archives and is ready
for training using the `train_model.py` module in the
[Augmented Chest X-Ray](https://github.com/MichaelNoya/augmented-chest-xray)
repository.

## The NIH Chest X-ray Dataset
The NIH Chest X-ray Dataset was introduced in ChestX-ray8 and later ChestX-ray14
by Wang et al.<sup id="ref1">[1](#foot1)</sup> It consists of 112,120 frontal view X-ray images of 30,805 unique patients with 14 common disease labels mined
using Natural Language Processing.

The dataset is provided by the NIH Clinical Center and can be downloaded at
this [link](https://nihcc.app.box.com/v/ChestXray-NIHCC).

## The Subset
The subset consists of 18,031 X-ray images of 5,000 unique patients. The images
were downscaled to 256x256 pixels and split into training, validation and
testing sets, ensuring no patient overlap between sets.

The subset was created using the `preprocess_data.py` module from the
[Augmented Chest X-Ray](https://github.com/MichaelNoya/augmented-chest-xray)
repository:
```shell
$ python preprocess_data.py -s 5000
```

## Accuracy of a Model Trained on the Subset
A model trained on the subset for 16 epochs reached its lowest validation loss
of 0.1657 after 14 epochs. The model achieved an AUROC of 0.782 on the provided
test set.

To better estimate the achieved accuracy, the model was additionally tested on
a separate larger test set (not included in this repository). The larger test
set consisted of 27,405 images from 7,500 patients with no patient overlap
between any of the mentioned sets. The model achieve an AUROC of 0.790 on the
larger test set.

Training and validation was performed using the `train_model.py` and
`validate_model.py` modules from the
[Augmented Chest X-Ray](https://github.com/MichaelNoya/augmented-chest-xray)
repository.

Training the model:
```shell
%run train_model.py -b 16 -w 2 -e 16 -l 0.001 -p 3 -a
```

Validation on the test set:
```shell
%run validate_model.py -b 32 -w 2 -c
```

## Reference <a name="reference"></a>

<b id="foot1">1.</b> [^](#ref1) Xiaosong Wang, Yifan Peng, Le Lu, Zhiyong Lu, Mohammadhadi Bagheri, Ronald Summers, ChestX-ray8: Hospital-scale Chest X-ray Database and Benchmarks on Weakly-Supervised Classification and Localization of Common Thorax Diseases, IEEE CVPR, pp. 3462-3471, 2017
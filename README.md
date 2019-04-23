## Quality Aware Network

Codebase for (Partial) [Quality Aware Network](https://arxiv.org/abs/1704.03373). Notice that QAN in ''Quality Aware Network for Set to Set Recognition'' is a 'single-part' version of P-QAN in ''Unsupervised Partial Quality Predictor for Large-Scale Person Re-identification'', so you can set part number to 1 if you wanna reproduce results of QAN.

**QAN** is used to handle set-to-set recognition problem. It can automatically learn the quality score for each sample in a set, and use the score to be the weight for synthesizing feature.

**P-QAN** is our subsequent work after QAN. It is used to handle video based person re-identification problem with awareness of partial quality. It can learn not only the quality of each frame but also the occlusion/blur/noise/etc. level in each part of a frame.

We use the [PRID 2011](https://lrs.icg.tugraz.at/datasets/prid/), [iLIDS-VID](www.eecs.qmul.ac.uk/.../downloads_qmul_iLIDS-VID_ReID_dataset.html) and [LPW] (coming soon) datasets for evaluation. They are video-based tasks for person re-identification.

## Running code

1.Clone [CaffeMex\_v2](https://github.com/sciencefans/CaffeMex_v2);

~~2.Replace `normalization layer (.hpp .cu .cpp)` in `CaffeMex_v2` with `layers/*` and add `NormalizationParameter` to `caffe.proto`;~~

3.Complile  with matlab interface (see readme in CaffeMex\_v2).

4.Configure the path `CaffeMex_v2/matlab/+caffe` to the directory in this project.

5.Configure the parameters in `train_baseline/train_baseline.m`, `train_baseline/train_LPW.m` and `train_PQAN/train_LPW.m`, `train_PQAN/train_network_and_test.m`, including the path of prototxt and the relative param. The pretrain_model can be found in here(https://github.com/lim0606/caffe-googlenet-bn).

6.Running the scripts in the `generate_data` to generate your dataset split.

7.Modify the number of corresponding network classifications.
Running the `train_baseline/train_baseline.m` or `train_baseline/train_LPW.m` for baseline and `train_PQAN/train_LPW.m`, `train_PQAN/train_network_and_test.m` for PQAN.

## Q&A

Here we list some commonly asked questions we received from the public. Thanks for your engagement to make our work better!

- *What is `LPW`?

 Labeled Pedestrian in the Wild (LPW) is a large scale human re-identification dataset that we collected in three different crowed scenes. ~~We haven't released it now but if you are interested in it, please contact us by e-mail.~~ Now you can download it at http://liuyu.us/dataset/lpw/.

- *Any strategies are used to make the quality scores effective?

 There are two main aspects that will affect the effectiveness of the quality scores. One is using a pre-trained model for imagenet classification task in order to make the network converge well. In the training stage, the use_global_stats is set to false in the Batchnorm layer; The other is the configuration of the parameter like learning rate, margin in the tripletloss layer, and you can adjust the parameters by observing the change of the scores in the training stage.

## Still having questions?
Feel free to drop us an email sharing your ideas.



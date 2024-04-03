# DeepFashion2 数据集
![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/deepfashion2_bigbang.png)

DeepFashion2 是一个全面的时尚数据集。它包含来自商业购物商店和消费者的 13 种流行服装类别共 49.1 万张不同的图像。总共拥有 80.1 万个服装项目，其中每张图像中的每个项目都被标记有比例、遮挡、放大、视角、类别、风格、边界框、密集地标和像素蒙版。还有 87.3 万个商业-消费者服装对。
该数据集被分为一个训练集（39.1 万张图像）、一个验证集（3.4 万张图像）和一个测试集（6.7 万张图像）。

<p align='center'>图 1：DeepFashion2 的示例。</p>

![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/annotation.jpg)

*<sub>从（1）到（4），每一行代表具有不同变化的服装图像。在每一行中，我们将图像分为两组，左边的三列代表来自商业商店的服装，而右边的三列则来自消费者。在每一组中，这三个图像表示对应变化的三个难度级别。此外，在每一行中，这两个组图像中的项目来自相同的服装身份，但来自两个不同的领域，即商业和消费者。相同身份的项目可能具有不同的风格，例如颜色和印刷。每个项目都带有地标和蒙版的注释。</sub>

# 公告
* **2020-2-6 我们正在 CVPR 2020 研讨会中举办DeepFashion2 挑战，包括[服装地标估计](https://competitions.codalab.org/competitions/22966)和[服装检索](https://competitions.codalab.org/competitions/22967)。详细信息可在[第三届计算机视觉用于时尚、艺术和设计研讨会](https://sites.google.com/view/cvcreative2020/home?authuser=0)中获取。**
* 2019-9-6 已发布的DeepFashion2 数据集的基线。
* 2019-8-1 2019 年 ICCV 研讨会中的DeepFashion2 挑战结束。
* 2019-7-12 由于 CodaLab 数据库的损坏，我们重新发布了DeepFashion2 挑战中的比赛。如果您是DeepFashion2 挑战的参与者，请重新创建一个帐户并在[地标估计](https://codalab.lri.fr/competitions/564)或[服装检索](https://codalab.lri.fr/competitions/565)中再次上传您的结果。
* 2019-7-1 DeepFashion2 的测试图像已在[DeepFashion2 数据集](https://drive.google.com/drive/folders/125F48fsMBz2EF0Cpqk6aaHet5VH399Ok?usp=sharing)中发布。（解压缩测试文件的密码与解压缩训练和验证文件的密码相同。）
* 2019-5-28 ICCV 2019 研讨会中的DeepFashion2 挑战的链接已发布。详细信息可在[第二届计算机视觉用于时尚、艺术和设计研讨会](https://sites.google.com/view/cvcreative/home?authuser=0)中获取。
* 2019-5-27 ICCV 2019 研讨会网站发布：[第二届计算机视觉用于时尚、艺术和设计研讨会](https://sites.google.com/view/cvcreative/home?authuser=0)。挑战的链接将很快发布。

# 下载数据
DeepFashion2 数据集可在[DeepFashion2 数据集](https://drive.google.com/drive/folders/125F48fsMBz2EF0Cpqk6aaHet5VH399Ok?usp=sharing)中获取。您需要填写[表格](https://docs.google.com/forms/d/e/1FAIpQLSeIoGaFfCQILrtIZPykkr8q_h9qQ5BoTYbjvf95aXbid0v2Bw/viewform?usp=sf_link)以获取解压缩文件的密码。请参阅下面的数据描述以获取有关数据集的详细信息。


# 数据组织
每个独立图像集中的图像都有一个独特的六位数字，例如 000001.jpg。相应的注释文件以 json 格式在注释集中提供，例如 000001.json。 
每个注释文件的组织方式如下： 
* **来源**：一个字符串，其中“商店”表示图像来自商业商店，而“用户”表示图像由用户拍摄。
* **对 ID**：一个数字。来自同一商店的图像及其相应的消费者拍摄的图像具有相同的对 ID。
  * 项目 1 
    * **类别名称**：一个表示物品类别的字符串。
    * **类别 ID**：一个与类别名称相对应的数字。在类别 ID 中，1 代表短袖上衣，2 代表长袖上衣，3 代表短袖外套，4 代表长袖外套，5 代表背心，6 代表吊带，7 代表短裤，8 代表裤子，9 代表裙子，10 代表短袖连衣裙，11 代表长袖连衣裙，12 代表背心裙，13 代表吊带裙。
    * **风格**：一个数字，用于区分具有相同对 ID 的图像中的服装项目。具有相同风格号码（大于 0）且来自具有相同对 ID 的图像的服装项目具有不同的风格，例如颜色、印刷和标志。这样，如果它们具有相同的风格号码且大于 0，并且它们来自具有相同对 ID 的图像，那么来自商店图像的服装项目和来自用户图像的服装项目就是正商业-消费者对。（如果您对风格感到困惑，请参考问题#10。） 
    * **边界框**：[x1,y1,x2,y2]，其中 x1 和 y_1 表示边界框的左上角点坐标，x_2 和 y_2 表示边界框的右下角点坐标。（宽度=x2-x1；高度=y2-y1）
    * **地标**：[x1,y1,v1,...xn,yn,vn]，其中 v 表示可见性：v=2 表示可见；v=1 表示遮挡；v=0 表示未标记。我们对不同类别的地标有不同的定义。地标注释的顺序在图 2 中列出。
    * **分割**：[[x1,y1,...xn,yn],[ ]]，其中 [x1,y1,xn,yn] 表示一个多边形，单个服装项目可能包含多个多边形。
    * **比例**：一个数字，其中 1 代表小比例，2 代表中等比例，3 代表大比例。
    * **遮挡**：一个数字，其中 1 代表轻微遮挡（包括无遮挡），2 代表中度遮挡，3 代表重度遮挡。
    * **缩放**：一个数字，其中 1 代表无缩放，2 代表中等缩放，3 代表大缩放。
    * **视图角度**：一个数字，其中 1 代表无穿着，2 代表正面视图，3 代表侧面或背面视图。
  * 项目 2 
 ...
<br>
  * 项目 n

请注意，'pair_id' 和 'ource' 是图像级别的标签。图像中的所有服装项目共享相同的'pair_id'和'source'。

13 类的地标和骨架的定义如下。图中的数字代表注释文件中每个类别的地标注释的顺序。总共定义了 294 个地标，涵盖了 13 个类别。

<p align='center'>图 2：地标和骨架的定义。</p>

![图片](https://github.com/switchablenorms/DeepFashion2/blob/master/images/cls.jpg)

我们不提供成对的数据。在训练数据集中，图像是按照连续的'pair_id'组织的，包括来自消费者的图像和来自商店的图像。（例如：000001.jpg（对 ID：1；来自消费者），000002.jpg（对 ID：1；来自商店），000003.jpg（对 ID：2；来自消费者），000004.jpg（对 ID：2；来自商店），000005.jpg（对 ID：2；来自消费者），000006.jpg（对 ID：2；来自商店），000007.jpg（对 ID：2；来自商店），000008.jpg（对 ID：2；来自商店）...）如果来自商店图像的服装项目和来自消费者图像的服装项目具有相同且大于 0 的风格号码，并且它们来自具有相同对 ID 的图像，则它们是正商业-消费者对，否则它们是负对。这样，您可以在实例级别构建训练正对和负对。

如图所示，前三个图像是来自消费者的，最后两个图像是来自商店的。这五张图像具有相同的“对 ID”。橙色边界框中的服装项目具有相同的“风格”：1。绿色边界框中的服装项目具有相同的“风格”：2。图中未绘制边界框的其他服装项目的“风格”为 0，它们无法构成正商业-消费者对。一个正商业-消费者对是第一个图像中标注的短袖上衣和最后一个图像中标注的短袖上衣。我们的数据集使得能够以灵活的方式在实例级别构建对。

![图片](https://github.com/switchablenorms/DeepFashion2/blob/master/images/pair.jpg)

# 数据描述
训练图像：train/image 训练标注：train/annos

验证图像：validation/image 验证标注：validation/annos

测试图像：test/image

每个单独图像集中的图像都有一个独特的六位数，例如 000001.jpg。相应的注释文件以 json 格式在注释集中提供，例如 000001.json。我们提供了代码从我们的数据集生成 coco 类型的标注，在[deepfashion2_to_coco.py](https://github.com/switchablenorms/DeepFashion2/blob/master/evaluation/deepfashion2_to_coco.py)中。请注意，在评估期间，图像_id 是图像名称中的数字。（例如，000001.jpg 的图像_id 是 1）。json 文件在 json_for_validation 和 json_for_test 中是根据上述规则使用[deepfashion2_to_coco.py](https://github.com/switchablenorms/DeepFashion2/blob/master/evaluation/deepfashion2_to_coco.py)生成的。通过这种方式，可以为评估中的服装检测任务和服装分割任务生成基准 json 文件，这些任务未在 DeepFashion2 挑战中列出。

在验证集中，我们在 keypoints_val_information.json、retrieval_val_consumer_information.json 和 retrieval_val_shop_information.json 中提供了图像级别的信息。（在验证集中，前 10844 张图像来自消费者，最后 20681 张图像来自商店。）对于未在 DeepFashion2 挑战中列出的服装检测任务和服装分割任务，keypoints_val_information.json 也可以使用。

我们为验证集的评估提供了 keypoints_val_vis.json、keypoints_val_vis_and_occ.json、val_query.json 和 val_gallery.json。您可以使用[评估代码](https://github.com/switchablenorms/DeepFashion2/blob/master/evaluation/evaluation.md)和上述 json 文件在本地获得验证分数。您也可以将结果提交到我们的 DeepFashion2 挑战的评估服务器。

在测试集中，我们在 keypoints_test_information.json、retrieval_test_consumer_information.json 和 retrieval_test_shop_information.json 中提供了图像级别的信息。（在测试集中，前 20681 张图像来自消费者，最后 41948 张图像来自商店。）您需要将结果提交到我们的 DeepFashion2 挑战的评估服务器。

# 数据集统计
表 1 显示了 DeepFashion2 中图像和标注的统计信息。（有关发布的图像和标注的统计信息，请参阅[DeepFashion2 挑战](https://sites.google.com/view/cvcreative/deepfashion2?authuser=0)）。

<p align='center'>表 1：DeepFashion2 的统计信息。</p>

| | 训练 | 验证 | 测试 | 总体 | 
|---:|---:|---:|---:|---:|
|图像|390,884|33,669|67,342|491,895|
|边界框|636,624|54,910|109,198|800,732|
|地标|636,624|54,910|109,198|800,732|
|掩码|636,624|54,910|109,198|800,732|
|对|685,584|查询：12,550<br/>图库：37183|查询：24,402<br/>图库：75,347|873,234|

图 3 显示了 DeepFashion2 中不同变化和 13 个类别中项目数量的统计信息。

<p align='center'>图 3：DeepFashion2 的统计信息。</p>

![图片](https://github.com/switchablenorms/DeepFashion2/blob/master/images/statistics_all.jpg)


# 基准
## 服装检测
该任务通过预测边界框和每个检测到的服装项目的类别标签来检测图像中的服装。
评估指标是边界框的平均精度<a href="https://www.codecogs.com/eqnedit.php?latex=$&space;{AP}_{box}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$&space;{AP}_{box}$" title="$ {AP}_{box}$" /></a>、<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{box}^{IoU=0.50}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{box}^{IoU=0.50}$" title="${AP}_{box}^{IoU=0.50}$" /></a>、<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{box}^{IoU=0.75}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{box}^{IoU=0.75}$" title="${AP}_{box}^{IoU=0.75}$" /></a>。

<p align='center'>表 2：使用发布的 DeepFashion2 数据集训练的服装检测在验证集上的评估。</p>

| AP | AP50 | AP75 | 
|---:|---:|---:|
|0.638|0.789|0.745|

<p align='center'>表 3：不同验证子集上的服装检测，包括比例、遮挡、放大和视角。</p>

|||<sub>比例|||<sub>遮挡|||<sub>放大|||<sub>视角||<sub>总体|
|:----:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||<sub>小|<sub>中等|<sub>大|<sub>轻微|<sub>中等|<sub>严重|<sub>无|<sub>中等|<sub>大|<sub>无穿着|<sub>正面|<sub>侧面或背面||
|<sub>AP|<sub>0.604|<sub>0.700|<sub>0.660|<sub>0.712|<sub>0.654|<sub>0.372|<sub>0.695|<sub>0.629|<sub>0.466|<sub>0.624|<sub>0.681|<sub>0.641|<sub>0.667|
|<sub>AP50|<sub>0.780|<sub>0.851|<sub>0.768|<sub>0.844|<sub>0.810|<sub>0.531|<sub>0.848|<sub>0.755|<sub>0.563|<sub>0.713|<sub>0.832|<sub>0.796|<sub>0.814|
|<sub>AP75|<sub>0.717|<sub>0.809|<sub>0.744|<sub>0.812|<sub>0.768|<sub>0.433|<sub>0.806|<sub>0.718|<sub>0.525|<sub>0.688|<sub>0.791|<sub>0.744|<sub>0.773



## 地标和姿势估计
该任务旨在预测每个检测到的服装项目在每张图像中的地标。同样，我们采用了 COCO 用于人体姿势估计的评估指标，通过计算关键点的平均精度<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{pt}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{pt}$" title="${AP}_{pt}$" /></a>、<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{pt}^{OKS=0.50}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{pt}^{OKS=0.50}$" title="${AP}_{pt}^{OKS=0.50}$" /></a>、<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{pt}^{OKS=0.75}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{pt}^{OKS=0.75}$" title="${AP}_{pt}^{OKS=0.75}$" /></a>，其中 OKS 表示物体地标相似性。

<p align='center'>表 4：使用发布的 DeepFashion2 数据集对验证集进行地标估计的训练结果。</p>

| | AP | AP50 | AP75 | 
|---:|---:|---:|---:|
|vis|0.605|0.790|0.684|
|vis && hide|0.529|0.775|0.596|

<p align='center'>表 5：不同验证子集上的地标估计，包括尺度、遮挡、放大和视角。每一行分别显示仅可见地标和可见和遮挡地标的评估结果</p>

|||<sub>Scale|||<sub>Occlusion|||<sub>Zoom_in|||<sub>Viewpoint||<sub>Overall|
|:----:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||<sub>small|<sub>moderate|<sub>large|<sub>slight|<sub>medium|<sub>heavy|<sub>no|<sub>medium|<sub>large|<sub>no wear|<sub>frontal|<sub>side or back||
 |<sub>AP|<sub>0.587<br/>0.497|<sub>0.687<br/>0.607|<sub>0.599<br/>0.555|<sub>0.669<br/>0.643|<sub>0.631<br/>0.530|<sub>0.398<br/>0.248|<sub>0.688<br/>0.616|<sub>0.559<br/>0.489|<sub>0.375<br/>0.319|<sub>0.527<br/>0.510|<sub>0.677<br/>0.596|<sub>0.536<br/>0.456|<sub>0.641<br/>0.563|
|<sub>AP50|<sub>0.780<br/>0.764|<sub>0.854<br/>0.839|<sub>0.782<br/>0.774|<sub>0.851<br/>0.847|<sub>0.813<br/>0.799|<sub>0.534<br/>0.479|<sub>0.855<br/>0.848|<sub>0.757<br/>0.744|<sub>0.571<br/>0.549|<sub>0.724<br/>0.716|<sub>0.846<br/>0.832|<sub>0.748<br/>0.727|<sub>0.820<br/>0.805|
|<sub>AP75|<sub>0.671<br/>0.551|<sub>0.779<br/>0.703|<sub>0.678<br/>0.625|<sub>0.760<br/>0.739|<sub>0.718<br/>0.600|<sub>0.440<br/>0.236|<sub>0.786<br/>0.714|<sub>0.633<br/>0.537|<sub>0.390<br/>0.307|<sub>0.571<br/>0.550|<sub>0.771<br/>0.684|<sub>0.610<br/>0.506|<sub>0.728<br/>0.641|


图 4 展示了地标和姿势估计的结果。

<p align='center'>图 4：地标和姿势估计的结果。</p>

![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/keys_vis.jpg)

## 服装分割
此任务为物品中的每个像素分配一个类别标签（包括背景标签）。评估指标是在掩码上计算的平均精度，包括<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{mask}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{mask}$" title="${AP}_{mask}$" /></a>、<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{mask}^{IoU=0.50}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{mask}^{IoU=0.50}$" title="${AP}_{mask}^{IoU=0.50}$" /></a>、<a href="https://www.codecogs.com/eqnedit.php?latex=${AP}_{mask}^{IoU=0.75}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?${AP}_{mask}^{IoU=0.75}$" title="${AP}_{mask}^{IoU=0.75}$" /></a>。

<p align='center'>表 6：使用已发布的 DeepFashion2 数据集训练的服装分割在验证集上的评估结果。</p>

| AP | AP50 | AP75 |
|---:|---:|---:|
|0.640|0.797|0.754|

<p align='center'>表 7：不同验证子集上的服装分割，包括尺度、遮挡、放大和视角。</p>

|||<sub>尺度|||<sub>遮挡|||<sub>放大|||<sub>视角||<sub>总体|
|:----:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||<sub>小|<sub>中等|<sub>大|<sub>轻微|<sub>中等|<sub>严重|<sub>无|<sub>中等|<sub>大|<sub>无磨损|<sub>正面|<sub>侧面或背面||
|<sub>AP|<sub>0.634|<sub>0.703|<sub>0.666|<sub>0.720|<sub>0.656|<sub>0.381|<sub>0.701|<sub>0.637|<sub>0.478|<sub>0.664|<sub>0.689|<sub>0.635|<sub>0.674|
|<sub>AP50|<sub>0.811|<sub>0.865|<sub>0.798|<sub>0.863|<sub>0.824|<sub>0.543|<sub>0.861|<sub>0.791|<sub>0.591|<sub>0.757|<sub>0.849|<sub>0.811|<sub>0.834|
|<sub>AP75|<sub>0.752|<sub>0.826|<sub>0.773|<sub>0.836|<sub>0.780|<sub>0.444|<sub>0.823|<sub>0.751|<sub>0.559|<sub>0.737|<sub>0.810|<sub>0.755|<sub>0.793| 

图 5 展示了服装分割的结果。

<p align='center'>图 5：服装分割的结果。</p>

![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/seg_vis.jpg) 


## 消费者到商店服装检索
对于从消费者拍摄的照片中检测到的项目，此任务旨在在图库中搜索与该检测到的项目相对应的商业图像。在这个任务中，采用 top-k 检索准确率作为评估指标。我们强调检索性能，同时仍然考虑检测器的影响。如果一件服装物品未能被检测到，则将该查询项目计为遗漏。

<p align='center'>表 8：使用检测框对发布的 DeepFashion2 数据集进行训练的消费者到商店服装检索在验证集上的评估。</p>

| |  top-1  |  top-5  |  top-10  |  top-15  |  top-20  |
|---:|---:|---:|---:|---:|---:|
|类别|0.079|0.198|0.273|0.329|0.366|
|关键点|0.182|0.326|0.416|0.469|0.510|
|分割|0.135|0.271|0.350|0.407|0.447|
|类别+关键点|0.192|0.345|0.435|0.488|0.524|
|类别+分割|0.152|0.295|0.379|0.435|0.477|

<p align='center'>表 9：在一些验证的消费者拍摄图像的不同子集上的消费者到商店服装检索。这些图像中的每个查询项目在验证商业图像中都有超过 5 个相同的服装项目。每行分别显示对地面实况框和检测到的框的评估结果。评估指标是 top-20 准确率。</p>

|||<sub>Scale|||<sub>Occlusion|||<sub>Zoom_in|||<sub>Viewpoint|||<sub>Overall||
|:----:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
||<sub>small|<sub>moderate|<sub>large|<sub>slight|<sub>medium|<sub>heavy|<sub>no|<sub>medium|<sub>large|<sub>no wear|<sub>frontal|<sub>side or back|<sub>top-1|<sub>top-10|<sub>top-20||
|<sub>class|<sub>0.520<br/>0.485|<sub>0.630<br/>0.537|<sub>0.540<br/>0.502|<sub>0.572<br/>0.527|<sub>0.563<br/>0.508|<sub>0.558<br/>0.383|<sub>0.618<br/>0.553|<sub>0.547<br/>0.496|<sub>0.444<br/>0.405|<sub>0.546<br/>0.499|<sub>0.584<br/>0.523|<sub>0.533<br/>0.487|<sub>0.102<br/>0.091|<sub>0.361<br/>0.312|<sub>0.470<br/>0.415|
|<sub>pose|<sub>0.721<br/>0.637|<sub>0.778<br/>0.702|<sub>0.735<br/>0.691|<sub>0.756<br/>0.710|<sub>0.737<br/>0.670|<sub>0.728<br/>0.580|<sub>0.775<br/>0.710|<sub>0.751<br/>0.701|<sub>0.621<br/>0.560|<sub>0.731<br/>0.690|<sub>0.763<br/>0.700|<sub>0.711<br/>0.645|<sub>0.264<br/>0.243|<sub>0.562<br/>0.497|<sub>0.654<br/>0.588|
|<sub>mask|<sub>0.624<br/>0.552|<sub>0.714<br/>0.657|<sub>0.646<br/>0.608|<sub>0.675<br/>0.639|<sub>0.651<br/>0.593|<sub>0.632<br/>0.555|<sub>0.711<br/>0.654|<sub>0.655<br/>0.613|<sub>0.526<br/>0.495|<sub>0.644<br/>0.615|<sub>0.682<br/>0.630|<sub>0.637<br/>0.565|<sub>0.193<br/>0.186|<sub>0.474<br/>0.422|<sub>0.571<br/>0.520|
|<sub>pose+class|<sub>0.752<br/>0.691|<sub>0.786<br/>0.730|<sub>0.733<br/>0.705|<sub>0.754<br/>0.725|<sub>0.750<br/>0.706|<sub>0.728<br/>0.605|<sub>0.789<br/>0.746|<sub>0.750<br/>0.709|<sub>0.620<br/>0.582|<sub>0.726<br/>0.699|<sub>0.771<br/>0.723|<sub>0.719<br/>0.684|<sub>0.268<br/>0.244|<sub>0.574<br/>0.522|<sub>0.665<br/>0.617|
|<sub>mask+class|<sub>0.656<br/>0.610|<sub>0.728<br/>0.666|<sub>0.687<br/>0.649|<sub>0.714<br/>0.676|<sub>0.676<br/>0.623|<sub>0.654<br/>0.549|<sub>0.725<br/>0.674|<sub>0.702<br/>0.655|<sub>0.565<br/>0.536|<sub>0.684<br/>0.648|<sub>0.712<br/>0.661|<sub>0.658<br/>0.604|<sub>0.212<br/>0.208|<sub>0.496<br/>0.451|<sub>0.595<br/>0.542|

图 6 展示了带有前五个检索到的服装项目的查询。第一列和第七列是由检测模块预测的带有边界框的客户图像，第二列到第六列和第八列到第十二列显示了商店的检索结果。

<p align='center'>图 6：服装检索的结果。</p>

![image](https://github.com/switchablenorms/DeepFashion2/blob/master/images/retrieval_vis.jpg)

# 引用
如果您在工作中使用了 DeepFashion2 数据集，请引用它如下：
```
@article{DeepFashion2,
  author = {Yuying Ge and Ruimao Zhang and Lingyun Wu and Xiaogang Wang and Xiaoou Tang and Ping Luo},
  title={一种多功能的基准，用于检测、姿势估计、分割和重新识别服装图像},
  journal={CVPR},
  year={2019}
}
```


## 使用的环境以及依赖
  ubuntu16.04   
  python3.6或python3.7  
  pytorch 1.3  torchvision 0.4    
  cuda 10.1  
  mmdetection框架  
  gcc >= 4.9  
  nccl 2  
  mmcv>=0.2.15    
  albumentations>=0.3.2  
  imagecorruptions  
  matplotlib  
  numpy  
  cython  
  pycocotools  
  six  
  terminaltables  
  
   
   
## 解决方案
 ### 数据集特点
 
  竞赛初赛阶段一的数据集图像尺寸最小为658x492，最大尺寸为4096x3000,所以，数据集的变化范围比较大；    
  
  针对训练集注释文件中只包含背景信息的图片，我们将其在注释文件中做删除处理，训练的过程中不予训练，目的是在目标检测过程中我们关心的是目标本身是否有瑕疵，所以训练的时候我们只训练目标本身，以达到更好的训练效果。 
  
 ### 模型选取
  该任务为多分类，多目标的任务，由于数据集中的图片数量比较少（千张级别）,选取的分类网络为ResNet50，检测网络为CascadeRcnn，所用网络模型为Cascade_rcnn_dconv_c3-c5_r50_fpn。
  
 ### 算法流程
 我们这次图像检测使用的是基于pytorch的mmdetection目标检测框架，使用的网络模型是基于Backbones为ResNet50的Cascade_rcnn_dconv_c3-c5_r50_fpn模型。  
 首先，我们针对数据集的特点，删除了数据集注释文件annotations.json文件中只有背景的图片（category_id = 0）,只训练了含有目标的图片；  
 其次，针对比赛要求的评价指标和IoU阈值，为了提高目标检测的准确度，我们对模型的配置文件进行了修改和设置，设置的地方如下：  
 
 **1、** epoch数，经过初赛阶段一的多次训练和测试，发现在epoch=18的时候训练比较充分，准确性比较高；  
  
 **2、** 经过实验我们发现/code/目录下的MyConfig.py 文件中model training and testing settings部分的阈值对实验结果产生了影响，根据比赛提供的IoU阈值，我们将网络配置文件MyConfig.py的rcnn的三个stage的阈值进行了设置，stage=1处的pos_iou_thr、neg_iou_thr、min_pos_iou分别为0.4，stage=2处的pos_iou_thr、neg_iou_thr、min_pos_iou设置成0.5，stage=3处的pos_iou_thr、neg_iou_thr、min_pos_iou设置成0.6（请看code目录下的MyConfig.py文件），这样的设置提高了检测框的准确性；  
 
 **3、** 在此基础上，我们设置配置文件（MyConfig.py）中model training and testing settings部分下的test_cfg下rcnn的score_thr，设置成0.003 ，此处的阈值设置也提高了准确性； 
 
 **4、** 其次，修改了配置文件中model training and testing settings部分下的rpn字典的pos_iou_thr由原来的0.7改成了0.6，neg_iou_thr和min_pos_iou由原来的0.3 改成0.2（请看code目录下的MyConfig.py文件）； 
 
 **5、** 针对数据集尺寸不相同的情况，我们在训练的过程中进行多尺度训练，经过实验证明，对图像进行1333x1000和1500x1200的尺寸训练得到的模型精度更高，泛化能力更强。    
 
 ## 代码运行说明
   ### 编译
   这个代码是基于mmdetection框架，代码所需的依赖位于/code/目录下的requirements.txt文件中，mmdet文件夹中是运行代码所需要的工具包，在依赖安装完成之后，需要执行编译，在/code/文件夹下，通过命令python setup.py develop 执行/code/目录下的编译文件setup.py，使程序进行编译。
 
  ### 程序入口
   所提交的代码project文件夹下面/code/目录下的main.py为主程序，执行python3 main.py即可产生预测结果，将在prediction_result目录下生成预测结果文件predictions.json，预测代码main.py根据/code/目录下的MyConfig.py文件和/usr_data/目录下的model.pth模型文件的内容共同产生预测结果predictions.json。
 
 

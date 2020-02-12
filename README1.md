## 使用的环境以及依赖
  ubuntu16.04   
  python3.6或python3.7  
  pytorch 1.3 torchvision 0.4    
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
  针对数据集尺寸不相同的情况，我们在训练的过程中进行多尺度训练，经过实验证明，对图像进行1333x1000和1500x1200的尺寸训练得到的模型训练精度更高，泛化能力更强。    
  针对训练集注释文件中只含有背景信息的图片标签，我们将其做删除处理，目的是在目标检测过程中我们关心的是目标本身是否有瑕疵，所以训练的时候我们只训练目标本身，已达到更好的训练效果。 
  
 ### 模型选取
  由于数据集中的图片数量比较少（千张级别）,所以选取
 ### 算法流程
 我们这次图像检测使用的是基于pytorch的mmdetection目标检测框架，使用的网络模型是基于Backbones为ResNet50的Cascade_rcnn_dconv_c3-c5_r50_fpn模型。  
 首先，我们针对数据集的特点，删除了数据集注释文件annotations.json文件中只有背景的图片（category_id = 0）,只训练了含有目标的图片；  
 其次，针对比赛要求的评价指标和IoU阈值，我们对模型的配置文件进行了修改，修改的地方如下：  
 **1、** epoch数，经过初赛阶段一的多次训练和测试，发现在epoch=18的时候精确性比较高；  
  
 **2、** 修改了模型配置文件中model training and testing settings部分，根据比赛提供的IoU阈值，我们将mmdetection下configs文件中cascade_rcnn_dconv_c3-c5_r50_fpn_1x.py文件下的rcnn的三个stage的阈值进行了修改，stage=1处的pos_iou_thr、neg_iou_thr、min_pos_iou由原来的0.5改成了0.4，stage=2处的pos_iou_thr、neg_iou_thr、min_pos_iou由原来的0.6改成了0.5，stage=3处的pos_iou_thr、neg_iou_thr、min_pos_iou由原来的0.7改成了0.6（请看code目录下的MyConfig.py文件）； 
 
 **3、** 在此基础上，我们修改了配置文件中model training and testing settings部分下的test_cfg下rcnn的score_thr，由原来的0.05改成了0.003； 
 
 **4、** 其次，修改了配置文件中model training and testing settings部分下的rpn字典的pos_iou_thr由原来的0.7改成了0.6，neg_iou_thr和min_pos_iou由原来的0.3 改成0.2（请看code目录下的MyConfig.py文件）； 
 
 ## 代码运行说明
   ### 编译
   这个代码是基于mmdetection框架，所以在依赖安装完成之后，需要执行编译，首先通过命令python setup.py develop 执行/code/目录下的setup.py文件，使程序进行编译。
 
  ### 程序入口
   所提交的代码中project文件夹下面/code/目录下的main.py为主程序，执行python3 main.py即可产生预测结果，将在prediction_result目录下生成预测结果文件predictions.json，预测代码main.py根据/code/目录下的MyConfig.py文件和/usr_data/目录下的model.pth模型文件的内容共同产生预测结果predjictions.json。
 
 

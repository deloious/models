 ## 解决方案
 ### 数据集特点
 竞赛初赛阶段一的数据集图像尺寸最小为658x492，最大尺寸为4096x3000,所以，数据集的变化范围比较大；
 其次，数据集中包含只有的背景图片，因此在训练的过程中需要将只含有背景的图片剔除到训练之外，使得模型的训练精度更高
 
 ## 模型转化指导
可以参考以下指导书将开源网络模型转化为华为NPU芯片支持的Davici模型。

[离线模型转化指导](https://ascend.github.io/ascenddk-private/doc/cn/mindstudio_opg/%E6%96%B0%E5%A2%9E%E8%87%AA%E5%AE%9A%E4%B9%89%E6%A8%A1%E5%9E%8B%E7%BB%84%E4%BB%B6.html)

## 模型列表<a name="section62083614491"></a>

<a name="table224171614494"></a>
<table><thead align="left"><tr id="row5243191618495"><th class="cellrowborder" valign="top" width="30%" id="mcps1.1.6.1.1"><p id="p1524371634910"><a name="p1524371634910"></a><a name="p1524371634910"></a>Model路径</p>
</th>
<th class="cellrowborder" valign="top" width="30%" id="mcps1.1.6.1.2"><p id="p82431216154918"><a name="p82431216154918"></a><a name="p82431216154918"></a>模型描述</p>
</th>
</th>

</tr>
</thead>
<tbody><tr id="row12243161634918"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.1.6.1.1 "><p id="p324351654911">computer_vision/object_detect/</p>
</td>
<td class="cellrowborder" valign="top" width="30%" headers="mcps1.1.6.1.2 "><p id="p15243916204916">此路径中模型为目标检测网络模型</p>
</td>
</tr>
<tr id="row12243161634918"><td class="cellrowborder" valign="top" width="30%" headers="mcps1.1.6.1.1 "><p id="p324351654911">computer_vision/classification/</p>
</td>
<td class="cellrowborder" valign="top" width="30%" headers="mcps1.1.6.1.2 "><p id="p15243916204916">此路径中模型为分类网络模型</p>
</td>
</tr>
</tbody>
</table>

## 说明<a name="section5806355565"></a>

模型提交请按照[README_MODEL_TEMPLATE.md](README_MODEL_TEMPLATE.md)要求提交。
此仓中的模型是从互联网获取的开源网络模型，未经过华为优化，相关精度、性能取决于源网络。如您不满足你的使用要求，可以联系华为获取商用解决方案。

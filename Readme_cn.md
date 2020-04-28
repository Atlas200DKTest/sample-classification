中文|[English](Readme.md)

# 分类网络应用（C++）<a name="ZH-CN_TOPIC_0232337690"></a>

本Application支��行在Atlas 200 DK或者AI加速云�务器上，实现了对常�的分类网络的推�功能并输出�n个推�结果。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="zh-cn_topic_0228461902_section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 部署<a name="zh-cn_topic_0228461902_section412811285117"></a>

�以选择如下快速部署或者常规方法部署，二选一��：

1.  快速部署，请�考：  [https://github.com/Atlas200dk/faster-deploy](https://github.com/Atlas200dk/faster-deploy)  。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   该快速部署脚本�以快速部署多个案例，请选择classification案例部署��。  
    >-   该快速部署脚本自动完�了代�下载�模型转��环境���置等�程，如果需�了解详细的部署过程请选择常规部署方�。转 **：[2. 常规部署](#zh-cn_topic_0228461902_li3208251440)**  

2.  <a name="zh-cn_topic_0228461902_li3208251440"></a>常规部署，请�考：  [https://github.com/Atlas200dk/sample-README/tree/master/sample-classification](https://github.com/Atlas200dk/sample-README/tree/master/sample-classification)  。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   该部署方�，需�手动完�代�下载�模型转��环境���置等过程。完��，会对其中的过程更加了解。  


## 编译<a name="zh-cn_topic_0228461902_section18931344873"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio。

    **./MindStudio.sh**

    �动�功�，打开**sample-classification**工程，如[图 打开classification工程](#zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig11106241192810)所示。

    **图 1**  打开classification工程<a name="zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig11106241192810"></a>  
    ![](figures/打开classification工程.png "打开classification工程")

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    **图 2**  �置文件路径<a name="zh-cn_topic_0228461902_fig0391184062214"></a>  
    ![](figures/�置文件路径.png "�置文件路径")

    该�置文件默认�置内容如下：

    ```
    remote_host=192.168.1.2
    model_name=alexnet.om
    ```

    -   remote\_host：Atlas 200 DK开�者�的IP地�。
    -   model\_name : 离线模型�称。
    -   如果�数和默认�置，�以修改为默认�置或者根�自己的实际ip与模型�称进行修改。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   �数必须全部填写，�则无法通过build。  
    >-   注��数填写时�需�使用“�符�。  
    >-   �置文件中�能填入�个模型�称，填入的模型为alexnet，用户�以使用常规部署列举的其它模型按照文档步骤进行替��行。  
    >-   当�已�按照�置示例�置默认值，请按照�置情况自行修改。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig478266192619)所示。

    **图 3**  执行deploy脚本<a name="zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig478266192619"></a>  
    ![](figures/执行deploy脚本.png "执行deploy脚本")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mind Studio工具，在工具�中点击**Build \> Build \> Build-Configuration**。如[图 编译�作�生�文件](#zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig1741464713019)所示，会在目录下生�build和run文件夹。

    **图 4**  编译�作�生�文件<a name="zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig1741464713019"></a>  
    ![](figures/编译�作�生�文件.png "编译�作�生�文件")

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  将需�推�的图片上传至Host侧任一属组为HwHiAiUser用户的目录。

    图片�求如下：

    -   格�：jpg�png�bmp。
    -   输入图片宽度：16px\~4096px之间的整数。
    -   输入图片高度：16px\~4096px之间的整数。


## �行<a name="zh-cn_topic_0228461902_section372782554919"></a>

1.  在Mind Studio工具的工具�中找到Run按钮，�击  **Run \> Run 'sample-classification'**，如[图 程�已执行示�图](#zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig93931954162719)所示，�执行程�已�在开�者�执行。

    **图 5**  程�已执行示�图<a name="zh-cn_topic_0228461902_zh-cn_topic_0203223265_fig93931954162719"></a>  
    ![](figures/程�已执行示�图.png "程�已执行示�图")

    以上报错信�请忽略，因为Mind Studio无法为�执行程�传�，上述步骤是将�执行程�与�赖的库文件部署到开�者�，此步骤需�ssh登录到开�者�至相应的目录文件下手动执行，具体请�考以下步骤。

2.  在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到Host侧。

    **ssh HwHiAiUser@**_host\_ip_

    对于Atlas 200 DK，host\_ip默认为192.168.1.2（USB连接）或者192.168.0.2（NIC连接），默认密�为Mind@123。

3.  进入通用分类网络应用的�执行文件所在路径。

    **cd \~/HIAI\_PROJECTS/workspace\_mind\_studio/sample-classification\_XXXXX/out**

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   此路径中sample-classification\_XXXXX的XXXXX是一串字�和数字的�机组�，�次�新编译�行时都会�机生�。  

4.  执行应用程�。

    执行**run\_classification.py**脚本会将推�结果在执行终端直接打�显示。

    命令示例如下所示：

    **python3 run\_classification.py -w  _227_   -h  _227_   -i** **_./example.jpg_  -n  _10_**

    -   -w/model\_width：模型的输入图片宽度，为16\~4096之间的整数，样例模型默认为227。
    -   -h/model\_height：模型的输入图片高度，为16\~4096之间的整数，样例模型默认为227。
    -   -i/input\_path：输入图片的路径，�以是目录，表示当�目录下的所有图片都作为输入（�以指定多个输入）。
    -   -n/top\_n：输出�n个推�结果。

    其他详细�数请执行**python3 run\_classification.py --help**命令��帮助信�。



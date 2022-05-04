## 一、安装python环境

略

## 二、安装Anaconda

- 前言
  - 就此项目而言，可自主选择安装与否
  - 不安装可直接看第三部分

- Anaconda的好处
  - Anaconda是一个打包的集合，里面包含了720多个数据科学相关的开源包，在数据可视化、机器学习、深度学习等多方面都有涉及。不仅可以做数据分析，还可以用在大数据和人工智能等领域。安装它后就默认安装了python、IPython、Jupyter notebook和集成开发环境 Spyder等等。
  - 并且，可以进行python环境的版本管理(允许用户方便地安装不同版本的python并可以快速切换)

- 安装教程

   - 可参考[这里](https://blog.csdn.net/qq_43529415/article/details/100847887)的第二部分
   - 注意点
     - 没有必要安装教程第三部分进行扩展(个人建议)
     - 检查Anaconda环境
       1. win+r键，输入cmd，确定
       2. 输入 conda --version
       3. 输入 anaconda --version
          ![图片](/image_readme/anaconda1.png)

     - 配置完配置完anaconda的环境变量后，win+r输入cmd ，打开cmd窗口后输入python显示的是anaconda的python版本，如果因为不习惯而需要换回原先系统的python解释器(此步可以不进行)，只需要在环境变量PATH中把系统python路径上移到anaconda之前即可。

       ​		![图片](/image_readme/anaconda2.png)

        完成之后效果

       ![图片](/image_readme/anaconda3.png)



## 三、安装CUDA cuDNN

- 检查自己电脑有无显卡

   - 检查方式：设备管理器 -> 显示适配器 即可看到显卡列表
   - 如有显卡，继续进行以下步骤; 如果没有，直接进行第四部分

 - 确定安装的CUDA版本：

    - 打开NVDIA控制面板

    - 进入后点击左下角系统信息即可看到

      ![图片](/image_readme/cuda1.png)

- CUDA cuDNN安装
  - [教程](https://blog.csdn.net/sinat_23619409/article/details/84202651)
  - 如果安装成功,恭喜你，可以直接进入第四步，若失败，以下是可能有用的解决方案
    	- 在自定义安装选项中 不勾选 Visual Studio Integration
    	- 上述方法仍然失败 请再 不勾选 Nsight Visual Studio Edision，Nsight NVTX
    	- 若仍然失败，可以参考[这个](https://blog.csdn.net/wuyanne/article/details/120823333)教程，但一定要确保你的显卡驱动可以重新安装回来，再进行此方法（最好先进行驱动备份）

## 安装pytorch环境

- python与CUDA对应版本
  - 在[这里](https://pytorch.org/get-started/previous-versions/)查找对应版本，例如 我安装的是CUDA11.0 那我就应该下载pytorch 1.7.1和torchvision 0.8.2
  - ![图片](/image_readme/pytorch1.png)

- 安装方法

  - 在线下载也好，离线安装的whl文件也罢，一定一定要记住选择cu版本，而不是cpu版本！安装了cpu版本，torch.cuda.is_available()返回是False。可以通过 pip list 查看自己有没有安装错，错了就pip uninstall，然后进行下列步骤
    - 无anaconda利用cmd安装
      - pip install torch\==1.7.1+cu101 torchvision==0.8.2+cu101 -f https://download.pytorch.org/whl/torch_stable.html -i https://pypi.tuna.tsinghua.edu.cn/simple some-package（-i 是国内镜像源 直接从官网下有点慢）
    - 无anaconda离线安装
      - 首先去[下载](https://download.pytorch.org/whl/torch_stable.html)对应版本whl文件，网页上面是cpu版本，记得往下滑，要记住下载的位置
      - 记得是两个whl文件 一个torch 一个torchvision
      - 打开cmd命令 cd进入该位置 使用pip进行安装
    - 有anaconda cmd命令安装
      	- 使用conda create 命令具体create格式前面应该有涉及,不做赘述
        - pip install --target=D:\anaconda\Anaconda3\envs\pytorch\Lib\site-packages torch\==1.7.1+cu101 torchvision==0.8.2+cu101 -f https://download.pytorch.org/whl/torch_stable.html -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
          (注释：直接使用pip install是安装到系统python中，而我们现在是要安装到虚拟环境中，所以安装指令一定要包含安装路径 --target部分 \pytorch 是我创建的虚拟环境名字 你们要改成对应虚拟环境的名字)
     - 有anaconda离线安装 
        - 结合上面的方法即可实现，不再赘述
   - 最后，检验是否安装成功
     	- 在cmd中输入python
     	- 输入import torch
     	- 输入torch.cuda.is_available()
     	-  如果是True 则说明安装完成

  ## 题外话

  - Conda 环境中 create命令是要在base环境下进行 如果在子环境下创建就套娃了；而且，这种情况下的虚拟环境使用conda remove -n xxx –all 命令是无效的 需要使用conda-env remove -p xxx -p 后面接的是路径 用conda info --envs 可以看到

    ![图片](/image_readme/last.png)

  - 想查看自己有没有安装错位置 也在对应环境下使用conda list 查看包 看看有没有相应的包名

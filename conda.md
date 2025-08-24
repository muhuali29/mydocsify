<h3 id="I29Lt">下载官网[https://www.anaconda.com/](https://www.anaconda.com/)，清华镜像源[https://mirrors.tuna.tsinghua.edu.cn/anaconda/](https://mirrors.tuna.tsinghua.edu.cn/anaconda/)，[https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/)</h3>


<h3 id="XLg2D">常用命令</h3>
conda init ，初始化后再用户目录C:\Users\wbb生成.condarc文件，编辑此文件填入，配置镜像源和环境目录

```plain
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults
show_channel_urls: true
envs_dirs:
  - D:\miniconda\envs                 
pkgs_dirs:
  - D:\miniconda\pkgs
```

conda info命令查看conda配置信息

![](https://cdn.nlark.com/yuque/0/2024/png/23024540/1730812862481-b3be5e62-262f-47b0-9d59-a3b1d561531e.png)如果不是writable需提升路径访问权限，步骤如下：

![](https://cdn.nlark.com/yuque/0/2024/png/23024540/1730812976532-1e0d8ad8-081b-4b5c-86bd-b22240c79e53.png)

![](https://cdn.nlark.com/yuque/0/2024/png/23024540/1730812993055-3a3132ab-c4c8-4d0d-a4ca-fab21f4a094b.png)`注意` ： **base environment : D:\dev software\miniconda3** 后面的 **(writable)** 非常重要，这说明权限更改完成，没有这一项会导致安装包的时候，报错显示无权限。  



创建虚拟环境

```plain
# 创建虚拟环境命令
conda create -n py39 python=3.9 

# 查看当前虚拟环境列表命令
conda env list

# 激活环境
conda activate env_name

# 退出当前激活的环境
conda deactivate

# 克隆环境
conda create --name new_env_name --clone old_env_name

删除环境
conda remove -n env_name --all

#显示包
conda  list

#查看conda的镜像源
conda config --show channels
```



<h1 id="BQvqj"></h1>





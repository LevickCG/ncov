# 西安电子科技大学晨午晚检自动填报工具

相比@Lincest@anadfox233 @Hon0nly的版本丰富了README.md，让不熟悉github action的同学也能轻松使用本工具。

> 使用步骤：
>
> - fork本项目
> - fork之后应该在**你的仓库页面**的Github-settings-secrets中设置对应帐号密码的secrets
>
> ![image-20200909222919501](./img/image-20200909222919501.png)
>
> 新建secret名称(NAME)为变量名，内容(VALUE)为变量的值。变量名应该与`.github/workflows/action.yml`中`secrets.***`一致。如果不想自定义可以用`NAME_NCOV`,`PSW_NCOR`作为学号、密码的变量名。
>
> ![image-20200909223214237](./img/image-20200909223214237.png)
>
> - 在项目页面中进入action
>
>   ![image-20210321085519307](./img/image-20210321085519307.png)
>
>   之后enable workflow. 然后就可以自动填报了。

## 注意
本脚本内置了南校区和北校区的经纬度,**默认定位为南校区**

> 其他地区, 请提交Issue

## 项目依赖
* python >= 3
* pip

运行以下命令来安装依赖包

```shell script
pip install -r requirements.txt
```

## 使用方法
1. 编写填写上传信息，格式如下。
> python 字典的语法, '#'以后为注释。各个参数与选项皆已列出,每一项都是必填字段
```python
{
    "sfzx": "1", # 是否在校(0->否, 1->是)
    "tw": "1", # 体温 (36℃->0, 36℃到36.5℃->1, 36.5℃到36.9℃->2, 36.9℃到37℃.3->3, 37.3℃到38℃->4, 38℃到38.5℃->5, 38.5℃到39℃->6, 39℃到40℃->7, 40℃以上->8)
    "sfcyglq": "0", # 是否处于隔离期? (0->否, 1->是)
    "sfyzz": "0", # 是否出现乏力、干咳、呼吸困难等症状？ (0->否, 1->是)
    "qtqk": "", # 其他情况 (文本)
    "askforleave": "0" # 是否请假外出? (0->否, 1->是)
}
```
2. 上报信息

默认情况下进行定时填报，但如果需要立即进行填报，请加入`-n 1`参数，例如：
```shell script
python upload.py -n 1 -c cookie路径 -l n -f 上报信息的文件路径
```

上报信息有2种方式: 
* 通过学号和密码提交信息, 系统会自动保存cookie到本地，下一次可以通过cookie上传信息 
* 凭借已经登录后的cookie提交信息(cookie的优先级大于学号密码)
> **脚本自身不记录任何学号和密码信息**

### 学号密码上报

```shell script
python upload.py -u 学号 -p 密码 -f 上报信息的文件路径
```

在不指定`-l`参数时默认上报南校区的GPS位置。

如需指定北校区，请添加`-l n`(north)，即以下命令

```shell script
python upload.py -u 学号 -p 密码 -l n -f 上报信息的文件路径
```

### cookie上报
```shell script
python upload.py -c cookie路径 -f 上报信息的文件路径
```

在不指定`-l`参数时默认上报南校区的GPS位置。

如需指定北校区，请添加`-l n`(north)，即以下命令

```shell script
python upload.py -c cookie路径 -l n -f 上报信息的文件路径
```

## 示例

### 用户名上报

![用户名上报](https://ning-wang.oss-cn-beijing.aliyuncs.com/blog-imags/用户名上报.gif)

### cookie上报

![cookie上报](https://ning-wang.oss-cn-beijing.aliyuncs.com/blog-imags/cookie上报.gif)


### Actions -build

![image-20200909223712295](./img/image-20200909223712295.png)

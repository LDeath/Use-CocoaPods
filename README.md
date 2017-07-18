
CocoaPods的使用  
=====
将自己的代码上传到CocoaPods上作为第三方使用

目录结构:
----
>git仓库目录<br>
>>LICENSE<br>
>>XXXXXXX<br>
>>XXXXXXX.podspec<br>
>>README.md<br>
>>Example<br>

LICENSE:          开源许可证,这里使用的是github自动创建的<br>
XXXXXXX:          开源代码的目录,<br>
xxxxxxx.podspec:  .podspec文件的作用是为了让CocoaPods搜索引擎知道该代码的作者、版本号、概要、描述、源代码地址、部署版本、依赖的框架等描述信息。<br>
README.md:        在github上创建时自带的说明文件,可有可无<br>
Example:          示例工程,可有可无<br>

一:创建git仓库<br>
   将要发布的代码上传到git,

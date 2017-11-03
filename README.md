
# CocoaPods的使用<br>

## 将自己的代码上传到CocoaPods上作为第三方使用<br>

在研究过程中，虽然百度了很多教程，但还是有一些坑不可避免的要踩，但又没有具体说明，这里把我碰到记录一下，主要有目录的结构如何构成，podspec文件如何编写（其实这个文件可以找一些成熟的三方库，将他们的文件改改就可），验证发布不通过的问题。
基本教程网上与很多，就不具体的说明了。

## 目录结构:<br>

>git仓库目录<br>
>>LICENSE<br>
>>XXXXXXX<br>
>>XXXXXXX.podspec<br>
>>README.md<br>
>>Example<br>  

LICENSE:开源许可证,这里使用的是github自动创建的<br>
XXXXXXX:开源框架需要包含的源文件目录,<br>
xxxxxxx.podspec:.podspec文件的作用是为了让CocoaPods搜索引擎知道该代码的作者、版本号、概要、描述、源代码地址、部署版本、依赖的框架等描述信息。<br>
README.md:在github上创建时自带的说明文件,可有可无<br>
Example:示例工程,可有可无<br> 
  创建.podspec文件,使用`pod spec create xxxx`命令创建.podspec文件<br>   
  
## .podspec文件说明<br>

Pod::Spec.new do |s|<br>
 s.name = "MAFShareTool"`开源框架在CocoaPods上可以搜索到的名称`<br>
 s.version = "0.1.3"`开源框架的版本`<br>
 s.summary = "常用分享封装"`简单描述`<br>
 s.description = <<-DESC<br>
		    对腾讯,微信,微博常用分享的简单封装<br>
                    DESC`详细描述`<br>
 s.homepage = "https://github.com/LDeath/ShareTool"`个人首页`<br>
 s.license = { :type => "MIT", :file => "LICENSE" }`开源许可证的指定`<br>
 s.author = { "xx" => "xxxxx@qq.com"}`作者描述`<br>
 s.ios.deployment_target = "7.0"`支持的ios版本`<br>
 s.source = { :git => "https://github.com/LDeath/ShareTool.git", :tag => s.version }`项目的地址`<br>
 s.source_files = 'MAFShareTool/**/**.{h,m}'`需要包含的源文件`<br>
 s.resource = 'MAFShareTool/Tencent/TencentOpenApi_IOS_Bundle.bundle'`若包含其他依赖的资源文件可这样填写`<br>
 s.ios.vendored_frameworks = 'MAFShareTool/Tencent/TencentOpenAPI.framework'`若包含其他依赖的库文件可这样填写`<br>
 s.frameworks = 'UIKit','Foundation','Security','SystemConfiguration','CoreGraphics','CoreTelephony'`依赖的系统库`<br>
 s.libraries = 'z','stdc++','sqlite3','iconv'`依赖的系统`<br>
 s.dependency 'WechatOpenSDK'`依赖的第三方库`<br>
 s.dependency 'WeiboSDK'`多个时分开填写`<br>
 end<br>
 ## 发布到CocoaPods<br>
重点来了，发布到CocoaPods需要通过验证才可以发布，在验证发布时碰到很多坑，由于不是当时写的这篇文章，具体情况忘记怎么样了：

但是在验证文件时总是会不通过，然后百度后加上了一些参数--verbose --use-libraries --allow-warnings，这样可以看验证时报的错误和警告，把错误处理一下，然后警告不影响验证，处不处理都无所谓，就可以通过验证了了。
 使用`pod spec lint xxxxxx.podspec --verbose --use-libraries --allow-warnings`命令来验证.podspec文件  
 `--verbose`显示验证时的详细信息 `--use-libraries`依赖库（s.dependency）包含了.a静态库会造成一些错误,虽然不影响Pod的使用,但是验证会不通过,使用此命令来让验证通过  `--allow-warnings`使用该命令来允许警告出现<br>
 
 在验证通过后，不要再使用普通命令来发布了，要跟在验证时的命令对应起来，即验证时使用的社么命令参数，在发布时也要加上，这样只要验证通过，一般都可成功发布到CocoaPods上了。
 验证通过后使用`pod trunk push xxxxxx.podspec --verbose --use-libraries --allow-warnings`命令来发布到CocoaPods
 
 发布成功后，通过pod search xxxx但是并有搜到是什么原因呢:
 这时需要更新你的本地仓库，将你发布到CocoaPods上的框架拉到本地仓库中即可搜到并正常使用了。

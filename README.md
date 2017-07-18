
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

LICENSE:开源许可证,这里使用的是github自动创建的<br>
XXXXXXX:开源框架需要包含的源文件目录,<br>
xxxxxxx.podspec:.podspec文件的作用是为了让CocoaPods搜索引擎知道该代码的作者、版本号、概要、描述、源代码地址、部署版本、依赖的框架等描述信息。<br>
README.md:在github上创建时自带的说明文件,可有可无<br>
Example:示例工程,可有可无<br>

.podspec文件说明
----
Pod::Spec.new do |s|<br>
 s.name = "MAFShareTool"  开源框架在CocoaPods上可以搜索到的名称<br>
 s.version = "0.1.3"         开源框架的版本<br>
 s.summary = "常用分享封装"   简单描述<br>
 s.description = <<-DESC<br>
		    对腾讯,微信,微博常用分享的简单封装<br>
                    DESC            详细描述<br>
 s.homepage = "https://github.com/LDeath/ShareTool"   个人首页<br>
 s.license = { :type => "MIT", :file => "LICENSE" }  开源许可证的指定<br>
 s.author = { "高赛" => "395765302@qq.com"}         作者描述<br>
 s.ios.deployment_target = "7.0"                                   支持的ios版本<br>
 s.source = { :git => "https://github.com/LDeath/ShareTool.git", :tag => s.version } 项目的地址<br>
 s.source_files = 'MAFShareTool/**/**.{h,m}'                                               需要包含的源文件<br>
 s.resource = 'MAFShareTool/Tencent/TencentOpenApi_IOS_Bundle.bundle'                  若包含其他依赖的资源文件可这样填写<br>
 s.ios.vendored_frameworks = 'MAFShareTool/Tencent/TencentOpenAPI.framework'                          若包含其他依赖的库文件可这样填写<br>
 s.frameworks = 'UIKit','Foundation','Security','SystemConfiguration','CoreGraphics','CoreTelephony' 依赖的系统库<br>
 s.libraries = 'z','stdc++','sqlite3','iconv'                                           依赖的系统<br>
 s.dependency 'WechatOpenSDK'    依赖的第三方库<br>
 s.dependency 'WeiboSDK'         多个时分开填写<br>

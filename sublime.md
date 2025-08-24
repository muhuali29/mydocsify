# Preferences菜单下添加package control子菜单，可手动安装和在线安装，在线安装不稳定，容易墙。
## 手动安装package control
1. Package Control安装不上的话可以手动安装package_control-master.zip
2. 直接解压，改名为Package Control，首字母大写
3. 打开Sublime Text 3，依次点击菜单“References”-“Browse Packages”  把Package Control文件夹直接拷贝到此目录
4. 重启Sublime Text，如果报错，返回上一层目录，既Sublime Text目录，找到Installed Packages文件夹打开
5. 把所有关于package control的文件都删了，重启Sublime Text
 
### 若遇到问题  弹出there are no pckages available for installation的对话框，解决方法如下
1. 添加channel_v3.json文件路径
2. 在Preferences->Package Setting->Package Control ->Setting User 中直接添加，我是直接放到d盘下面了
3. 例如"channels": [
		 "d:/channel_v3.json"
	 ],
6. 或者使用sublime中文网在线地址"channels": [ "http://packagecontrol.cn/channel_v3.json" ]


## 在线安装package control
1. 第一步：通过控制台安装插件代码，通过 ctrl+` 或 View > Show Console打开控制台，将Python代码粘贴到控制台，回车。
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.cn/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
2. 第二步：修改Sublime Text插件channels，方法如下：打开Package Control配置文件Setting-user添加
"channels": [ "http://packagecontrol.cn/channel_v3.json" ]
保存搞定



# package control 安装成功后  按 ctrl+shift+p  输入install Package 并选择，在输入插件名安装插件
## 例如以下几个
1.HTML-CSS-JS Prettify
2.SublimeCodeIntel
3.a file icon
4.sublimelinter
5.AutoFileName



# 安装emmet和vim
### 首选项-浏览插件目录把VintageEx文件夹放入与users同级
然后再到Preferentces-Seetings添加如下：
{
	"ignored_packages":
	[],
	"vintage_start_in_command_mode": true
}
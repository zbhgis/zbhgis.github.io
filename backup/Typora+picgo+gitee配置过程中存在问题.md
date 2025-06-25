# Typora+picgo+gitee配置过程中存在问题

1、刚开始是使用GitHub，但是不知道为什么一直上传不了图片，找了很多的解决方法都没能成功，考虑到可能是网络等方方面面的问题，于是放弃了GitHub，选择了Gitee；参考以下[[博客](https://blog.csdn.net/weixin_45525272/article/details/125387761)](https://blog.csdn.net/weixin_45525272/article/details/125387761)(https://blog.csdn.net/weixin_45525272/article/details/125387761)；
2、在配置Gitee中的过程中，除了需要注册好Gitee，建立好仓库、需要保管好私人令牌外，还需要提前安装好node.js环境，直接去官网下载最新的长期支持版本即可；
3、在线安装Gitee的picgo插件过程中，插件一直显示安装中，即一直安装不上，这个时候就需要先前往picgo文件夹下的 node_moudules先将安装失败的插件文件夹 picgo-plugin-gitee-uploader 删除，然后再通过以下[[博客](https://blog.csdn.net/Netceor/article/details/126704416)](https://blog.csdn.net/Netceor/article/details/126704416)的方法(https://blog.csdn.net/Netceor/article/details/126704416)，通过命令行的方式进行安装；

![image-20231007161015722](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231007161015722.png)

4、如果中间安装失败，哪一步卡住，可以先尝试重启应用然后再重新执行操作，可以避免一些不必要的问题。
<!-- ##{"timestamp":1696949773}## -->
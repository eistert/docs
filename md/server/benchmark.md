# 性能测试
1. 修改最大文件打开数（ulimit），修改方法请用百度查。
2. 单独部署db，并对配置进行优化。
3. 下载jmeter3.3版本。把```tools/jmeter/*.jar```放到```\pathtojmeter\lib\ext```。
4. 使用jmeter打开```tools/jmeter/```目录下的连接数和发送消息脚本进行测试。注意进行连接数测试时需要使用jmeter集群模式，或者多台测试机器同时开始，以便能够达到理想的测试结果。
#启动
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
#关闭
sudo launchctl unload -w /System/Library/LaunchDaemons/ssh.plist
#查看
sudo launchctl list | grep ssh



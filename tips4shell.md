shell 實用小技巧
=================

### IPv4 address 判斷

    找出/etc/hosts 中含有IP 的文字列
    grep -E '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /etc/hosts
    
    取出/etc/hosts 中含有IP 的部分
    grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /etc/hosts
    
    用bash判斷字串是否為IPV4
    if [ ` echo $ip | grep -E '^((25[0-5]|2[0-4][0-9]|[01]?[1-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[1-9][0-9]?)$'  | grep -o "\." | wc -l` -eq 3 ];
    then 
        ipv4=true
    else 
        ipv4=false
    fi


參考來源: 

1. [What regular expression can I use to match an IP address?](http://superuser.com/questions/202818/what-regular-expression-can-i-use-to-match-an-ip-address)
2. [Shell 搭配正規式來檢測一字串是否為IPv4 格式之IP](http://www.rtfiber.com.tw/~changyj/shell/check_ip.pdf)


### sed: 將找到字串存起來, 取出

    sed -n 's/\(La\)/\1Oo/p' dataf3
    把找到的 La 存起來，用 \1 取回來使用
    sed -i 取代修改原始檔
    
參考來源: [[Linux] sed replace 指令](http://xiao-ming-chang.blogspot.tw/2013/06/linux-sed-replace.html)


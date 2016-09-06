shell script 實用小技巧
=======================
---
### IPv4 address 判斷

    找出/etc/hosts 中含有IP 的文字列
    grep -E '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /etc/hosts
    
    取出/etc/hosts 中含有IP 的部分
    grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /etc/hosts
    
    用bash判斷字串是否為IPV4
    if [ ` echo $ip | grep -E '^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$'  | grep -o "\." | wc -l` -eq 3 ];
    then 
        ipv4=true
    else 
        ipv4=false
    fi


參考來源: 

1. [What regular expression can I use to match an IP address?](http://superuser.com/questions/202818/what-regular-expression-can-i-use-to-match-an-ip-address)
2. [Shell 搭配正規式來檢測一字串是否為IPv4 格式之IP](http://www.rtfiber.com.tw/~changyj/shell/check_ip.pdf)

---
### sed: 將找到字串存起來, 取出

    sed -n 's/\(La\)/\1Oo/p' dataf3
    把找到的 La 存起來，用 \1 取回來使用
    sed -i 取代修改原始檔
    
參考來源: [[Linux] sed replace 指令](http://xiao-ming-chang.blogspot.tw/2013/06/linux-sed-replace.html)

---
### for i = 0 to 6, 或者 a to z 之使用方法

    for i in {0..6}; do
        echo $i
    done

    for i in {a..z}; do
        echo $i
    done


參考來源: [Armbian](https://github.com/igorpecovnik/lib)

---

### 將命令列之參數轉換成 shell 內部的變數

    $ cat test.sh
    ## Script parameters handling
    for i in "$@"; do
	    if [[ $i == *=* ]]; then
		    parameter=${i%%=*}
		    value=${i##*=}
		    echo "Command line: setting $parameter to ${value:-(empty)}"
		    eval $parameter=$value
	    fi
    done
    
    $ test.sh KERNEL=new COLOR=red Loop=3 DEFAULT_VAR=
    則在 test.sh 經過上面的for-loop 之後, 就會產生4個變數分別為:
    KERNEL=new 
    COLOR=red 
    Loop=3 
    DEFAULT_VAR=

參考來源: [Armbian](https://github.com/igorpecovnik/lib)

---

### 判斷 debian/ubuntu 是否已經安裝某個套件

    判斷是否已經安裝了'git' 套件, 若沒有, 則使用 apt-get 來安裝'git'
    
    [[ $(dpkg-query -W -f='${db:Status-Abbrev}\n' git 2>/dev/null) != *ii* ]] && \
    apt-get -qq -y --no-install-recommends install git

參考來源: [Armbian](https://github.com/igorpecovnik/lib)

---

### 檢查是否有 root 權限

    檢查是否有 root 權限, 若沒有, 則離開程式.
    
    if [[ $EUID != 0 ]]; then
        echo -e "[\e[0;35m warn \x1B[0m] This script requires root privileges"
        sudo "$0" "$@"
        exit $?
    fi
    
參考來源: [Armbian](https://github.com/igorpecovnik/lib)


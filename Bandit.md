0 -> 1
ssh bandit0@bandit.labs.overthewire.org -p 2220

bandit1: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

./- ： 当前目录下的-文件

bandit2:PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

cat "./文件名"
cat -- "文件名"

bandit3:7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

bandit4:xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

cat -- *

bandit5:6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

find . -size 1033c -exec cat {} \;

bandit6:pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

find / -size 33c -group bandit6 -user bandit7 -exec cat {} \;

bandit7:Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

grep "millionth" data.txt

bandit8:VR1ljMayciFxbnUokuQmJFw6QC9VKtub

sort data.txt | uniq -u
把sort得到的结果用 ｜ 交给uniq(可以判断相邻行重复)，-u是只出现一次的意思

bandit9:EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

strings data.txt | grep "="

bandit10:B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

cat data.txt | base64 --decode
或者写成base64 -d

bandit11:pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
意思是把，A到Z和a到z，一一映射到，N到Z和A到M和n到z和a到m

bandit12:GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

mktemp -d
会自动创建一个随机名字的临时目录。

xxd -r data.txt > data
xxd     把文件转换成十六进制形式
xxd -r  reverse，反过来把十六进制恢复成原始二进制

file 文件
    ↓
看看是什么类型
    ↓
gzip → gzip -d
bzip2 → bzip2 -d
tar → tar -xf
    ↓
file 新文件
    ↓
继续……

xxd -r data.txt > data
file data

mv data data.gz
gzip -d data.gz
file data

mv data data.bz2
bzip2 -d data.bz2
file data

mv data data.gz
gzip -d data.gz
file data

mv data data.tar
tar -xf data.tar
ls

bandit13:qQYQiHOBPR8zR61qxYqX45quvihF2uzk

bandit14用sshkey
ssh -i 密钥.key ……

bandit14:aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

nc localhost 30000
输入……
nc是普通的TCP
给本机的30000端口发点啥东西

bandit15:pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

openssl s_client -connect localhost:30001
openssl是TLS 加密的 TCP

bandit16:kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V


先扫描：
```
nmap -p 31000-32000 localhost
```
看到若干类似：
```
PORT      STATE SERVICE
31xxx/tcp open  unknown
31xxx/tcp open  unknown
...
```
```
openssl s_client -connect localhost:PORT -quiet
```
然后输入当前 `bandit16` 密码。

diff passwords.old passwords.new

bandit18:OQxXZjELndr90zuhOTDYBEomI0SZITXI

bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
提前输入命令防止被踢掉

bandit19:KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI

./bandit20-do cat /etc/bandit_pass/bandit20
这个脚本可以获得bandit20的身份

bandit20:4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA

nc -l 12345 监听这个端口，等待连接
./suconnect 12345 对这个端口执行命令

bandit21:bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY

cron
 ↓
以 bandit22 身份运行脚本
 ↓
读取 /etc/bandit_pass/bandit22
 ↓
把密码写到 /tmp/某个文件
 ↓
chmod 644
 ↓
其他用户也可以读取

bandit22:RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz

echo I am user bandit23 
↓
生成一段字符串 
md5sum 
↓
算这段字符串的 MD5 
cut -d ' '-f 1 
↓
只取 MD5 哈希本身

bandit23:gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw

cat > /tmp/getbandit24.sh <<EOF cat在没有文件名时读取输入原样输出，`<<EOF`：告诉 shell，接下来一直读输入，直到遇到单独一行 `EOF` 为止。
#!/bin/bash
cat /etc/bandit_pass/bandit24 > "$outfile"
EOF

bandit24:hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv

PASS='你的 bandit24 密码'

for pin in $(seq -w 0 9999); do
    echo "$PASS $pin"
done | nc localhost 30002 | grep -v "Wrong"
done表示循环结束

bandit25:SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P

bandit27:STJLJBRRphMxKB392CT4iOr5CbzPU9ER

bandit28:y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ

bandit29:Em7eGtqaMySwNFjCpwzzHhLhospOcdt0

bandit30:jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX

bandit31:82NkymblpGBYmIXG6ZQ8YldBYstHpfUf

bandit32:pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT

bandit33:u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM


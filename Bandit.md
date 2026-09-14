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


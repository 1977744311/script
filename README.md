# script
1. demo.sh是一个可以快速创建一个基本的网页结构的脚本，是用shell语言编写。
2. demo.js是用node语言编写的与demo.sh实现同样的功能。
3. gpo是我自己编写的可以快速git到远程仓库的脚本。
4. z.sh脚本是一个可以快速跳转到指定目录的脚本。

下面是具体的使用步骤：
## demo.sh
1. 找个地方新建文件，后缀随意，一般来说脚本的后缀是 .sh。我喜欢把脚本放在 ~/local 目录里。
```
   mkdir ~/local
   cd ~/local
   touch demo.txt
```
2. 编辑 demo.txt，内容如下：
```
  mkdir demo
  cd demo
  mkdir css js
  touch index.html css/style.css js/main.js
  exit
```
3. 给 demo.sh 添加执行权限（windows用户可以省略这一步）
```
   chmod +x demo.txt
```
4. 在任意位置执行 `sh ~/local/demo.txt` 即可运行
5. 将 ~/local 添加到 PATH 里
```
cd ~/local; pwd //得到local的绝对路径
touch ~/.bashrc //创建 ~/.bashrc
start ~/.bashrc //编辑 ~/.bashrc,在最后一行添加 export PATH="local的绝对路径:$PATH"
source ~/.bashrc //保存配置
demo.txt //脚本成功运行
```
6. demo.txt 的后缀 .txt 很无聊，删掉它
```
mv ~/local/demo.txt ~/local/demo
```
现在你只要运行 demo 就能执行该脚本了。

### 改进版
增加了判断目录是否存在，且可以自定义目录名，代码如下：
```
if [ -d $1 ]; then
  echo 'error: dir exists'
  exit
else
  mkdir $1
  cd $1
  mkdir css js
  touch index.html css/style.css js/main.js
  echo 'success'
  exit
fi
```
## demo.js
原理和用shell编写一样，只不过语句变为node的形式。代码如下：
```
var fs = require('fs')

 var dirName = process.argv[2] // 你传的参数是从第 2 个开始的

 fs.mkdirSync("./" + dirName) // mkdir $1
 process.chdir("./" + dirName) // cd $1
 fs.mkdirSync('css') // mkdir css
 fs.mkdirSync('js') // mkdir js

 fs.writeFileSync("./index.html", "")
 fs.writeFileSync("css/style.css", "")
 fs.writeFileSync("./js/main.js", "")

 process.exit(0)
 ```
 最后运行此脚本使用如下代码：
 ```
 node ~/local/demo.js zzz //创建一个zzz目录的文件
 ```
 要想使node脚本像shell脚本一样不用输前缀的话，则需要在代码的第一行加上：
 ```
 #!/usr/bin/env node
 ```
 这样的话，就不用每次加上node了，如果你的PATH配置好了，那就可以直接输入`demo.js 你的目录名`。
 
 ## gpo 
 

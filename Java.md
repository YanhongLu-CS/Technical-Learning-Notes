brew install openjdk@21
`openjdk@21`：安装 Java 21 的 OpenJDK
安装完成后，JDK 通常会放在 Homebrew 自己的目录里，比如 Apple Silicon Mac 上一般类似：
```
/opt/homebrew/opt/openjdk@21
```

sudo ln -sfn $HOMEBREW_PREFIX/opt/openjdk@21/libexec/openjdk.jdk \
/Library/Java/JavaVirtualMachines/openjdk-21.jdk
在 macOS 标准的 Java 目录里，创建一个指向 Homebrew JDK 的**符号链接**。
最终这条命令相当于建立：
```
/Library/Java/JavaVirtualMachines/openjdk-21.jdk
        ↓
Homebrew 安装的真实 openjdk.jdk
```


echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 21)' >> ~/.zshrc
echo 'export PATH="$JAVA_HOME/bin:$PATH"' >> ~/.zshrc
`.zshrc` 是 zsh 的配置文件。Mac 现在默认 shell 通常是 zsh，每次打开新的 Terminal，zsh 都会读取这个文件。
所以把 `JAVA_HOME` 写进去以后，以后每次打开 Terminal 都会自动配置。


source ~/.zshrc

java -version
javac -version
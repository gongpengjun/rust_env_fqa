# Rust env FQA

collect FQA while setup and maintain rust develop environment, on Mac mostly

## 问题："Too many open files"

#### 问题现象

```
thread '<unnamed>' panicked at 'failed to open /dev/urandom: Os { code: 24, kind: Other, message: "Too many open files" }', src/libcore/result.rs:999:5
note: Run with `RUST_BACKTRACE=1` environment variable to display a backtrace.
thread 'main' panicked at 'failed to start new Runtime: Os { code: 24, kind: Other, message: "Too many open files" }', src/libcore/result.rs:999:5
```

#### 问题原因

```
$ launchctl limit maxfiles
	maxfiles    256            unlimited
$ ulimit -n
256
```

#### 解决方法


```
sudo launchctl limit maxfiles 10000000 10000000
ulimit -n 4096000
```

操作示例：

```
$ sudo launchctl limit maxfiles 10000000 10000000
Password:
$ launchctl limit maxfiles
	maxfiles    10000000       10000000    
$ ulimit -n 4096000
$ ulimit -n
4096000
```



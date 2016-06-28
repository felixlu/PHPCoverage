﻿# PHPCoverage说明文档
PHPCoverage是一款基于xdebug实现的PHP代码覆盖率统计工具，可以方便地对PHP项目的代码覆盖率情况进行统计。


### 使用
PHPCoverage的使用非常简单，在下载了PHPCoverage的项目代码至本地后，只需在项目的主入口处（通常是项目的index.php文件的开头处）引用插桩文件，并添加插桩代码即可。

##### 插桩代码的示例如下：
```javascript
// 引入插桩文件，例如我的本地PHPCoverage项目位置在：/vagrant/github/PHPCoverage
require '/vagrant/github/PHPCoverage/Injecter.php';

// 插桩
PHPCoverage_Inject([
    'log_dir'=>'/vagrant/logs/PHPCoverage',
    'ignore_file'=>'/vagrant/github/PHPCoverage/ignores/example.ignore',
    'is_repeat' => true 
]);
```

##### 参数说明：
###### log_dir
log_dir应该是一个PHP具有写权限的目录，用于生成覆盖率统计文件及最终的覆盖率报告。

###### ignore_file
ignore_file用于指定需要忽略掉的文件，比如第三方的代码、框架文件以及其他不想关注的文件。
该文件`使用PHP数组描述`，在PHPCoverage项目的ignores文件夹中包含一个示例文件example.ignore

###### is_repeat
is_repeat可以指定为ture或false，用于控制是否进行`叠加测试`。
当is_repeat为false时，将不进行叠加测试，这意味着每次开始执行测试之前，都会清空log_dir目录中的所有文件（即之前的测试记录）。
当is_repeat为true时，将进行叠加测试，这意味着多次测试生成的文件将会被保留，并最终进行合并分析。
如果想对单次PHP请求的代码覆盖率情况进行统计，应该将is_repeat设为false。
如果想要统计多次代码执行累计的代码覆盖率情况，则应该讲is_repeat设为true。
也可以手工清除log_dir中的内容以保证之前的测试结果不会被之后的测试一起统计。


## 使用
### 使用Composer安装使用


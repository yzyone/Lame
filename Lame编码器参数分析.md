
# lame编码器参数分析 #

---

lame命令格式

    lame [options] inputfile [outputfile]//参数 输入文件 输出文件

（1）CBR

    lame --freeformat -b <N(128kbps)> sample.wav/sample.mp3 //无论输入是wav文件还是MP3文件，都可以编码成固定码率的MP3文件
    lame sample.wav  sample.mp3//默认为32kbps
    lame -h sample.wav  sample.mp3//高质量编码，128kbps联合立体声（-h相当于-q2）（-q0-->-q9）
    lame -f sample.wav  sample.mp3//快速编码，低质量，无噪声（-f相当于-q7）（不推荐）
    lame -b n sample.wav  sample.mp3//以n码率编码

（2）ABR

    lame -h --abr <N(128kbps)>  sample.wav sample.mp3//围绕N的平均码率编码

（3）VBR

	lame -V2 sample.wav sample.mp3//V0压缩率最低相当于最高质量(质量大约是CBR质量的256kbps)，V9压缩率最高相当于质量最差

    -v//以VBR编码
    -V n//vbr质量设置n从0到9
    -b n//指定最小用的比特率，例：lame -v -b 112  input.wav output.mp3，如果文件太大，则lame -v -V n -b 112  input.wav output.mp3（n从0到9），
    如果想用尽可能大的压缩比率，可以尝试lame -v  input.wav output.mp3或者lame -v -V n input.wav output.mp3
    -B n//指定最大用的比特率（不推荐）
    --vbr-old//用旧式vbr路线
    --vbr-new//用新式vbr编码

（4）MP3解码

    --decode//把MP3文件解压成wav文件，输入可以是任何编码中承认的任何格式，输出是没有wav头的PCM信号

（5）编码模式

	-m m           mono单通道
	-m s           stereo立体声
	-m j           joint stereo联合立体声
	-m f           forced mid/side stereo
	-m d           dual (independent) channels独立双通道
	-m i           intensity stereo强烈立体声
	-m a           auto自动转换

如果输入是立体PCM信号，要编码成单通道，则lame -m s -a
如果输入是wav或者aiff格式的源文件，编码成单通道，则lame -m m，用这个参数，即便双通道的也会变成单通道

（6）其他参数

	-s n  //输入采样频率
	--resample  n //输出采样频率
	--replaygain-fast  //快速播放增益分析
	-r //即假设输入为未加工的PCM信号，如果没有此参数，怎会从wav或者AIFF文件头中查找相应的参数
	-q n  //量化选择，n从0到9
	-p  //CRC矫正，此参数只适用于lame编码器
	-o   //把编码过的文件当做副本
	--noreplaygain  //取消增益分析与--replaygain-accurate, --replaygain-fast对应
	--nohist  //VBR中，编码器会自动生成直方图，此参数代表取消生成直方图
	--mp3input  //代表输入是MP3文件，编码器会会对其先进行解码，在编码
	--clipdetect  //剪切检测
	-c   //编码版权
	-x  //输入文件，交换比特

 

来源：[http://www.cnblogs.com/macong/archive/2012/11/15/2771413.html](http://www.cnblogs.com/macong/archive/2012/11/15/2771413.html)
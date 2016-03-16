#FFMPEG COMPILATION GUIDE FOR MAC OS X
#FFMPEG -MAC编译指南

#####以下内容翻译自[FFMPEG/Wiki/CompilationGuide/MacOSX](htts://trac.ffmpeg.org/CompilationGuide/MacOSX)
######原网址可能需要翻墙

#####[Wiki](https://trac.ffmpeg.org/wiki):[CompilationGuide](https://trac.ffmpeg.org/wiki/CompilationGuide)/[MacOSX](https://trac.ffmpeg.org/wiki/CompilationGuide/MacOSX)

####在OS X上编译FFmpeg有以下几种方法。
#####1.自行编译。
######在Mac OS X上编译和在其他Unix机器上编译一样简单，但是有几个警告。常规流程是获取源代码->`./configure <flags>`->`make && sudo make install`，只需输入指定的flags就可以了。
#####2.工具编译。
######另一种方法可以用一些"编译助手"工具来帮助你编译安装FFmpeg。比如[Homebrew](http://brew.sh/)和[macports](https://www.macports.org/)。具体步骤请查看本文[Homebrew章节](https://github.com/Kito0615/Translations/blob/master/CompilationGuideForMacOS.md#通过homebrew安装ffmpeg)。
#####3.下载安装。
######如果你不能编译或者你也不想安装Homebrew，你可以直接下载[FFmpeg For OS X稳定版](https://ffmpeg.org/download.html)，但是，有可能并不包含一些你想要的功能。典型的就是需要你解压文件[如.zip文件]，然后在刚解压出来的文件夹中找到FFmpeg程序路径，运行它。
--
####通过Homebrew安装FFmpeg
######[Homebrew](http://brew.sh/)是一个安装包管理器命令行，与分布式Linux系统上的`apt-get`方式十分类似。要使用Homebrew，你需要先安装`brew`，如果你还没有安装，请使用以下命令安装
######`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
######如果安装成功，输入以下命令以最少配置选项(和依赖库)安装最新版本的FFmpeg:
######`brew install ffmpeg`
######这些安装包的版本都是Homebrew的方案(formulas)，安装程序会自动将FFmpeg的依赖库安装好。你可以输入`brew info ffmpeg`查看额外的安装选项，如：如果想要添加`libfdk_aac`或`libvpx`两个库(这两个库是高度推荐安装的)，可以输入以下包含额外推荐选项的命令:
######`brew install ffmpeg --with-fdk-aac --with-ffplay --with-freetype --with-libass --with-libquvi --with-libvorbis --with-libvpx --with-opus --with-x265`
######如果你不清楚怎么配置和编译二进制文件，你会发现使用Homebrew相当简单。以后如果要升级FFmpeg到最新版本时，只需要输入以下命令即可:
######`brew update && brew upgrade ffmpeg`
######如果你想通过Homebrew安装FFmpeg的最新Git版本，在第一条安装命令后面添加`--HEAD`，如：
######`brew install ffmpeg <install_options_if_desired> --HEAD`
######如果你想手动编译FFmpeg的最新Git版本，请继续往下阅读。
####手动编译FFmpeg
#####使用Xcode编译
######从Mac OS X 10.7开始，Xcode已经在Mac App Store上可以免费下载了，并且在Mac上编译任何东西都需要用到它。请确保你已经通过`Xcode->Preferences(command+,)->Downloads->Components`安装了Command Line Tools.早期的版本需要一个AppleID和免费的开发者账户，可以在[developer.apple.com](https://developer.apple.com/)注册。
#####使用Homebrew编译
######要获取Mac OS X的FFmpeg，首先，你需要安装[Homebrew](http://brew.sh)。如果你不想安装Homebrew，请阅读下一节。Homebrew安装命令:
######`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
######然后输入以下命令:
######`brew install automake fdk-aac git lam libass libtool libvorbis libvpx \ opus sdl shtool texi2html theora wget x264 xvid yasm`
######Mac OS X从10.7版本开始已经自带Freetype(早期版本可以需要在安装过程中选择'X11'，通常情况下X11的路径是:`/usr/X11`)。然后在终端运行`freetype-config`就会显示出独立的文件夹，像头文件(headers)，库文件(libraries)，所以，请在输入`./configure`配置命令之前，运行以下命令或将以下命令添加到`$HOME/.profile`文件中:
######`CFLAGS='freetype-config --cflags' LDFLAGS='freetype-config --libs' PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig:/usr/lib/pkgconfig:/usr/X11/lib/pkgconfig`
#####不使用Homebrew手动安装FFmpeg依赖库
#####-Pkg-config & GLib
######Pkg-config是检查可以被编译进ffmpeg的库的必要文件，它需要GLib，但是GLib并没有安装在Mac OS X(绝大多数Unix系统中都安装了)系统中。你可能需要下载pkg-config 0.23,或从[Gnome.org](http://ftp.gnome.org/pub/GNOME/sources/glib/)下载压缩文件解压并编译它。pkg-config可以从[Freedesktop.org](http://pkgconfig.freedesktop.org/releases/)下载。
######要编译GLib，你还要从[GNU.org](ftp://ftp.gnu.org/gnu/gettext/)下载gettext，并且编辑stpncpy.c文件，在"#ifndef weak_alias"前加一行"#undef stpncpy"。Mac OS X从10.7开始有它自己版本的stpncopy功能(不兼容)，在gettext里重复了。正常编译gettext就行了。使用以下命令编译GLib:
######`LIBFFI_CFLAGS=-I/usr/include/ffi LIBFFI_LIBS=-lffi`
######`./configure`
######`make && sudo make install`(这一步时，可能需要输入管理员密码)
######要编译pkg-config，输入以下命令:
######`GLIB_FLAGS="-I/usr/local/include/glib-2.0 -I/usr/local/lib/glib-2.0/include" GLIB_LIBS="-lglib-2.0 -lgio-2.0"`
######`./configure --with-pc-path="/usr/X11/lib/pkgconfig:/usr/X11/share/pkgconfig:/usr/local/pkgconfig"`
#####-Yasm
######Yasm可以从[tortall.net](http://yasm.tortall.net/Download.html)下载，Yasm是编译包含机器独立汇编代码的C代码必要文件。使用以下命令安装Yasm:
######`./configure --enable-python`
######`make && sudo make install`(这一步，可能需要输入管理员密码)
#####-额外依赖库
######以下仅仅只是举例，具体参数请输入`./configure --help`查看:
######	*[x264](http://www.videolan.org/developers/x264.html) 编码H.264视频。编译参数`--enable-gpl --enable-libx264`
######	*[fdk-aac](https://sourceforge.net/projects/opencore-amr/files/fdk-aac/)编码AAC音频。编译参数`--enable-libfdk-aac`
######	*[libvpx](https://code.google.com/p/webm/downloads/list)。VP8/VP9视频编码器。编译参数`--enable-libvpx`
######	*[libvorbis](http://downloads.xiph.org/releases/vorbis/) 编码Vorbis音频。需要[libogg](http://downloads.xiph.org/releases/ogg/)。编译参数`--enable-libvorbis`
######	*[libopus](http://www.opus-codec.org/downloads/)编码Opus音频。
######	*[LAME](https://sourceforge.net/projects/lame/files/lame/)编码MP3音频。编译参数`--enable-libmp3lame`
######	*[libass](https://github.com/libass/libass)字幕渲染器。编译参数`--enable-libass`
#####正式编译
######如果你已经编译好了所有你想要的编码器/依赖库，你就可以使用Git下载FFmpeg的源代码或者从网站链接下载发布的压缩文件。研究`./configure --help`的输出，确保你已经启用了所有你想要功能，记住`--enable-nonfree`和`--enable-gpl`两个参数将是上面某些库的依赖条件。下面是一个编译例子:
######`git clone http://source.ffmpeg.org/git/ffmpeg.git ffmpeg`
######`cd ffmpeg`
######`./configure --prefix=/usr/local --enable-gpl --enable-nonfree --enable-libass\`
######`--enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libopus \`
######`--enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libxvid`
######`make && sudo make install`



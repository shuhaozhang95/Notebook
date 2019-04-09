# Linux/Unix

#### _什么是Shell?_

shell 就是一个程序，它接受从键盘输入的命令， 然后把命令传递给操作系统去执行。几乎所有的 Linux 发行版都提供一个名为 bash 的 来自 GNU 项目的 shell 程序。bash 是最初 Unix 上由 Steve Bourne 写成 shell 程序 sh 的增强版。

#### _终端仿真器_ <a id="&#x7EC8;&#x7AEF;&#x4EFF;&#x771F;&#x5668;"></a>

当使用图形用户界面时，我们需要另一个和 shell 交互的叫做终端仿真器的程序。 如果我们浏览一下桌面菜单，可能会找到一个。虽然在菜单里它可能都 被简单地称为 “terminal”，但是 KDE 用的是 konsole , 而 GNOME 则使用 gnome-terminal。 还有其他一些终端仿真器可供 Linux 使用，但基本上，它们都完成同样的事情， 让我们能访问 shell。也许，你可能会因为附加的一系列花俏功能而喜欢上某个终端。

#### _命令历史_ <a id="&#x547D;&#x4EE4;&#x5386;&#x53F2;"></a>

如果按下上箭头按键，我们会看到刚才输入的命令“kaekfjaeifj”重新出现在提示符之后。 这就叫做命令历史。许多 Linux 发行版默认保存最后输入的500个命令。 按下下箭头按键，先前输入的命令就消失了。

* pwd — 打印出当前工作目录名
* cd — 更改目录
* ls — 列出目录内容

类似于 Windows，一个“类 Unix” 的操作系统，比如说 Linux，以分层目录结构来组织所有文件。 这就意味着所有文件组成了一棵树型目录（有时候在其它系统中叫做文件夹）， 这个目录树可能包含文件和其它的目录。文件系统中的第一级目录称为根目录。 根目录包含文件和子目录，子目录包含更多的文件和子目录，依此类推。

注意\(类 Unix 系统\)不像 Windows ，每个存储设备都有一个独自的文件系统。类 Unix 操作系统， 比如 Linux，总是只有一个单一的文件系统树，不管有多少个磁盘或者存储设备连接到计算机上。 根据负责维护系统安全的系统管理员的兴致，存储设备连接到（或着更精确些，是挂载到）目录树的各个节点上。

#### 绝对路径 <a id="&#x7EDD;&#x5BF9;&#x8DEF;&#x5F84;"></a>

绝对路径开始于根目录，紧跟着目录树的一个个分支，一直到达所期望的目录或文件。 例如，你的系统中有一个目录，大多数系统程序都安装在这个目录下。这个目录的 路径名是 /usr/bin。它意味着从根目录（用开头的“/”表示）开始，有一个叫 “usr” 的 目录包含了目录 “bin”。

#### 相对路径 <a id="&#x76F8;&#x5BF9;&#x8DEF;&#x5F84;"></a>

绝对路径从根目录开始，直到它的目的地，而相对路径开始于工作目录。 为了做到这个（用相对路径表示）， 我们在文件系统树中用一对特殊符号来表示相对位置。 这对特殊符号是 “.” \(点\) 和 “..” \(点点\)。

符号 “.” 指的是工作目录，”..” 指的是工作目录的父目录。下面的例子说明怎样使用它。 让我们再次把工作目录切换到 /usr/bin：

| 表3-1: cd 快捷键 |  |
| :--- | :--- |
| 快捷键 | 运行结果 |
| cd | 更改工作目录到你的家目录。 |
| cd - | 更改工作目录到先前的工作目录。 |
| cd ~user\_name | 更改工作目录到用户家目录。例如, cd ~bob 会更改工作目录到用户“bob”的家目录。 |

#### 关于文件名的重要规则

1. 以 “.” 字符开头的文件名是隐藏文件。这仅表示，ls 命令不能列出它们， 用 ls -a 命令就可以了。当你创建帐号后，几个配置帐号的隐藏文件被放置在 你的家目录下。稍后，我们会仔细研究一些隐藏文件，来定制你的系统环境。 另外，一些应用程序也会把它们的配置文件以隐藏文件的形式放在你的家目录下面。
2. 文件名和命令名是大小写敏感的。文件名 “File1” 和 “file1” 是指两个不同的文件名。
3. Linux 没有“文件扩展名”的概念，不像其它一些系统。可以用你喜欢的任何名字 来给文件起名。文件内容或用途由其它方法来决定。虽然类 Unix 的操作系统， 不用文件扩展名来决定文件的内容或用途，但是有些应用程序会。
4. 虽然 Linux 支持长文件名，文件名可能包含空格，标点符号，但标点符号仅限 使用 “.”，“－”，下划线。最重要的是，不要在文件名中使用空格。如果你想表示词与 词间的空格，用下划线字符来代替。过些时候，你会感激自己这样做。

| 表 4-1: ls 命令选项 |  |  |
| :--- | :--- | :--- |
| 选项 | 长选项 | 描述 |
| -a | --all | 列出所有文件，甚至包括文件名以圆点开头的默认会被隐藏的隐藏文件。 |
| -d | --directory | 通常，如果指定了目录名，ls 命令会列出这个目录中的内容，而不是目录本身。 把这个选项与 -l 选项结合使用，可以看到所指定目录的详细信息，而不是目录中的内容。 |
| -F | --classify | 这个选项会在每个所列出的名字后面加上一个指示符。例如，如果名字是 目录名，则会加上一个'/'字符。 |
| -h | --human-readable | 当以长格式列出时，以人们可读的格式，而不是以字节数来显示文件的大小。 |
| -l |  | 以长格式显示结果。 |
| -r | --reverse | 以相反的顺序来显示结果。通常，ls 命令的输出结果按照字母升序排列。 |
| -S |  | 命令输出结果按照文件大小来排序。 |
| -t |  | 按照修改时间来排序。 |

#### 确定文件类型 <a id="&#x786E;&#x5B9A;&#x6587;&#x4EF6;&#x7C7B;&#x578B;"></a>

file filename

#### 用 less 浏览文件内容 <a id="&#x7528;-less-&#x6D4F;&#x89C8;&#x6587;&#x4EF6;&#x5185;&#x5BB9;"></a>

less filename

一旦 less 程序运行起来，我们就能浏览文件内容了。如果文件内容多于一页，那么我们可以上下滚动文件。按下“q”键， 退出 less 程序。

下表列出了 less 程序最常使用的键盘命令。

| 表 4-3: less 命令 |  |
| :--- | :--- |
| 命令 | 行为 |
| Page UP or b | 向上翻滚一页 |
| Page Down or space | 向下翻滚一页 |
| UP Arrow | 向上翻滚一行 |
| Down Arrow | 向下翻滚一行 |
| G | 移动到最后一行 |
| 1G or g | 移动到开头一行 |
| /charaters | 向前查找指定的字符串 |
| n | 向前查找下一个出现的字符串，这个字符串是之前所指定查找的 |
| h | 显示帮助屏幕 |
| q | 退出 less 程序 |

  

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x8868; 4-4: Linux &#x7CFB;&#x7EDF;&#x4E2D;&#x7684;&#x76EE;&#x5F55;</th>
      <th
      style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x76EE;&#x5F55;</td>
      <td style="text-align:left">&#x8BC4;&#x8BBA;</td>
    </tr>
    <tr>
      <td style="text-align:left">/</td>
      <td style="text-align:left">&#x6839;&#x76EE;&#x5F55;&#xFF0C;&#x4E07;&#x7269;&#x8D77;&#x6E90;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/bin</td>
      <td style="text-align:left">&#x5305;&#x542B;&#x7CFB;&#x7EDF;&#x542F;&#x52A8;&#x548C;&#x8FD0;&#x884C;&#x6240;&#x5FC5;&#x987B;&#x7684;&#x4E8C;&#x8FDB;&#x5236;&#x7A0B;&#x5E8F;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/boot</td>
      <td style="text-align:left">
        <p>&#x5305;&#x542B; Linux &#x5185;&#x6838;&#x3001;&#x521D;&#x59CB; RAM &#x78C1;&#x76D8;&#x6620;&#x50CF;&#xFF08;&#x7528;&#x4E8E;&#x542F;&#x52A8;&#x65F6;&#x6240;&#x9700;&#x7684;&#x9A71;&#x52A8;&#xFF09;&#x548C;
          &#x542F;&#x52A8;&#x52A0;&#x8F7D;&#x7A0B;&#x5E8F;&#x3002;</p>
        <p>&#x6709;&#x8DA3;&#x7684;&#x6587;&#x4EF6;&#xFF1A;</p>
        <ul>
          <li>/boot/grub/grub.conf or menu.lst&#xFF0C; &#x88AB;&#x7528;&#x6765;&#x914D;&#x7F6E;&#x542F;&#x52A8;&#x52A0;&#x8F7D;&#x7A0B;&#x5E8F;&#x3002;</li>
          <li>/boot/vmlinuz&#xFF0C;Linux &#x5185;&#x6838;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">/dev</td>
      <td style="text-align:left">&#x8FD9;&#x662F;&#x4E00;&#x4E2A;&#x5305;&#x542B;&#x8BBE;&#x5907;&#x7ED3;&#x70B9;&#x7684;&#x7279;&#x6B8A;&#x76EE;&#x5F55;&#x3002;&#x201C;&#x4E00;&#x5207;&#x90FD;&#x662F;&#x6587;&#x4EF6;&#x201D;&#xFF0C;&#x4E5F;&#x9002;&#x7528;&#x4E8E;&#x8BBE;&#x5907;&#x3002;
        &#x5728;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x91CC;&#xFF0C;&#x5185;&#x6838;&#x7EF4;&#x62A4;&#x7740;&#x6240;&#x6709;&#x8BBE;&#x5907;&#x7684;&#x5217;&#x8868;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/etc</td>
      <td style="text-align:left">
        <p>&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x5305;&#x542B;&#x6240;&#x6709;&#x7CFB;&#x7EDF;&#x5C42;&#x9762;&#x7684;&#x914D;&#x7F6E;&#x6587;&#x4EF6;&#x3002;&#x5B83;&#x4E5F;&#x5305;&#x542B;&#x4E00;&#x7CFB;&#x5217;&#x7684;
          shell &#x811A;&#x672C;&#xFF0C; &#x5728;&#x7CFB;&#x7EDF;&#x542F;&#x52A8;&#x65F6;&#xFF0C;&#x8FD9;&#x4E9B;&#x811A;&#x672C;&#x4F1A;&#x5F00;&#x542F;&#x6BCF;&#x4E2A;&#x7CFB;&#x7EDF;&#x670D;&#x52A1;&#x3002;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x4E2D;&#x7684;&#x4EFB;&#x4F55;&#x6587;&#x4EF6;&#x5E94;&#x8BE5;&#x662F;&#x53EF;&#x8BFB;&#x7684;&#x6587;&#x672C;&#x6587;&#x4EF6;&#x3002;</p>
        <p>&#x6709;&#x8DA3;&#x7684;&#x6587;&#x4EF6;&#xFF1A;&#x867D;&#x7136;/etc &#x76EE;&#x5F55;&#x4E2D;&#x7684;&#x4EFB;&#x4F55;&#x6587;&#x4EF6;&#x90FD;&#x6709;&#x8DA3;&#xFF0C;&#x4F46;&#x8FD9;&#x91CC;&#x53EA;&#x5217;&#x51FA;&#x4E86;&#x4E00;&#x4E9B;&#x6211;&#x4E00;&#x76F4;&#x559C;&#x6B22;&#x7684;&#x6587;&#x4EF6;&#xFF1A;</p>
        <ul>
          <li>/etc/crontab&#xFF0C; &#x5B9A;&#x4E49;&#x81EA;&#x52A8;&#x8FD0;&#x884C;&#x7684;&#x4EFB;&#x52A1;&#x3002;</li>
          <li>/etc/fstab&#xFF0C;&#x5305;&#x542B;&#x5B58;&#x50A8;&#x8BBE;&#x5907;&#x7684;&#x5217;&#x8868;&#xFF0C;&#x4EE5;&#x53CA;&#x4E0E;&#x4ED6;&#x4EEC;&#x76F8;&#x5173;&#x7684;&#x6302;&#x8F7D;&#x70B9;&#x3002;</li>
          <li>/etc/passwd&#xFF0C;&#x5305;&#x542B;&#x7528;&#x6237;&#x5E10;&#x53F7;&#x5217;&#x8868;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">/home</td>
      <td style="text-align:left">&#x5728;&#x901A;&#x5E38;&#x7684;&#x914D;&#x7F6E;&#x73AF;&#x5883;&#x4E0B;&#xFF0C;&#x7CFB;&#x7EDF;&#x4F1A;&#x5728;/home
        &#x4E0B;&#xFF0C;&#x7ED9;&#x6BCF;&#x4E2A;&#x7528;&#x6237;&#x5206;&#x914D;&#x4E00;&#x4E2A;&#x76EE;&#x5F55;&#x3002;&#x666E;&#x901A;&#x7528;&#x6237;&#x53EA;&#x80FD;
        &#x5728;&#x81EA;&#x5DF1;&#x7684;&#x76EE;&#x5F55;&#x4E0B;&#x5199;&#x6587;&#x4EF6;&#x3002;&#x8FD9;&#x4E2A;&#x9650;&#x5236;&#x4FDD;&#x62A4;&#x7CFB;&#x7EDF;&#x514D;&#x53D7;&#x9519;&#x8BEF;&#x7684;&#x7528;&#x6237;&#x6D3B;&#x52A8;&#x7834;&#x574F;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/lib</td>
      <td style="text-align:left">&#x5305;&#x542B;&#x6838;&#x5FC3;&#x7CFB;&#x7EDF;&#x7A0B;&#x5E8F;&#x6240;&#x4F7F;&#x7528;&#x7684;&#x5171;&#x4EAB;&#x5E93;&#x6587;&#x4EF6;&#x3002;&#x8FD9;&#x4E9B;&#x6587;&#x4EF6;&#x4E0E;
        Windows &#x4E2D;&#x7684;&#x52A8;&#x6001;&#x94FE;&#x63A5;&#x5E93;&#x76F8;&#x4F3C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/lost+found</td>
      <td style="text-align:left">&#x6BCF;&#x4E2A;&#x4F7F;&#x7528; Linux &#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x7684;&#x683C;&#x5F0F;&#x5316;&#x5206;&#x533A;&#x6216;&#x8BBE;&#x5907;&#xFF0C;&#x4F8B;&#x5982;
        ext3&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#xFF0C; &#x90FD;&#x4F1A;&#x6709;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x3002;&#x5F53;&#x90E8;&#x5206;&#x6062;&#x590D;&#x4E00;&#x4E2A;&#x635F;&#x574F;&#x7684;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x65F6;&#xFF0C;&#x4F1A;&#x7528;&#x5230;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x3002;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x5E94;&#x8BE5;&#x662F;&#x7A7A;&#x7684;&#xFF0C;&#x9664;&#x975E;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;
        &#x771F;&#x6B63;&#x7684;&#x635F;&#x574F;&#x4E86;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/media</td>
      <td style="text-align:left">&#x5728;&#x73B0;&#x5728;&#x7684; Linux &#x7CFB;&#x7EDF;&#x4E2D;&#xFF0C;/media
        &#x76EE;&#x5F55;&#x4F1A;&#x5305;&#x542B;&#x53EF;&#x79FB;&#x52A8;&#x4ECB;&#x8D28;&#x7684;&#x6302;&#x8F7D;&#x70B9;&#xFF0C;
        &#x4F8B;&#x5982; USB &#x9A71;&#x52A8;&#x5668;&#xFF0C;CD-ROMs &#x7B49;&#x7B49;&#x3002;&#x8FD9;&#x4E9B;&#x4ECB;&#x8D28;&#x8FDE;&#x63A5;&#x5230;&#x8BA1;&#x7B97;&#x673A;&#x4E4B;&#x540E;&#xFF0C;&#x4F1A;&#x81EA;&#x52A8;&#x5730;&#x6302;&#x8F7D;&#x5230;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x7ED3;&#x70B9;&#x4E0B;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/mnt</td>
      <td style="text-align:left">&#x5728;&#x65E9;&#x4E9B;&#x7684; Linux &#x7CFB;&#x7EDF;&#x4E2D;&#xFF0C;/mnt
        &#x76EE;&#x5F55;&#x5305;&#x542B;&#x53EF;&#x79FB;&#x52A8;&#x4ECB;&#x8D28;&#x7684;&#x6302;&#x8F7D;&#x70B9;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/opt</td>
      <td style="text-align:left">&#x8FD9;&#x4E2A;/opt &#x76EE;&#x5F55;&#x88AB;&#x7528;&#x6765;&#x5B89;&#x88C5;&#x201C;&#x53EF;&#x9009;&#x7684;&#x201D;&#x8F6F;&#x4EF6;&#x3002;&#x8FD9;&#x4E2A;&#x4E3B;&#x8981;&#x7528;&#x6765;&#x5B58;&#x50A8;&#x53EF;&#x80FD;
        &#x5B89;&#x88C5;&#x5728;&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;&#x5546;&#x4E1A;&#x8F6F;&#x4EF6;&#x4EA7;&#x54C1;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/proc</td>
      <td style="text-align:left">&#x8FD9;&#x4E2A;/proc &#x76EE;&#x5F55;&#x5F88;&#x7279;&#x6B8A;&#x3002;&#x4ECE;&#x5B58;&#x50A8;&#x5728;&#x786C;&#x76D8;&#x4E0A;&#x7684;&#x6587;&#x4EF6;&#x7684;&#x610F;&#x4E49;&#x4E0A;&#x8BF4;&#xFF0C;&#x5B83;&#x4E0D;&#x662F;&#x771F;&#x6B63;&#x7684;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x3002;
        &#x76F8;&#x53CD;&#xFF0C;&#x5B83;&#x662F;&#x4E00;&#x4E2A;&#x7531; Linux
        &#x5185;&#x6838;&#x7EF4;&#x62A4;&#x7684;&#x865A;&#x62DF;&#x6587;&#x4EF6;&#x7CFB;&#x7EDF;&#x3002;&#x5B83;&#x6240;&#x5305;&#x542B;&#x7684;&#x6587;&#x4EF6;&#x662F;&#x5185;&#x6838;&#x7684;&#x7AA5;&#x89C6;&#x5B54;&#x3002;&#x8FD9;&#x4E9B;&#x6587;&#x4EF6;&#x662F;&#x53EF;&#x8BFB;&#x7684;&#xFF0C;
        &#x5B83;&#x4EEC;&#x4F1A;&#x544A;&#x8BC9;&#x4F60;&#x5185;&#x6838;&#x662F;&#x600E;&#x6837;&#x76D1;&#x7BA1;&#x8BA1;&#x7B97;&#x673A;&#x7684;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/root</td>
      <td style="text-align:left">root &#x5E10;&#x6237;&#x7684;&#x5BB6;&#x76EE;&#x5F55;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/sbin</td>
      <td style="text-align:left">&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x5305;&#x542B;&#x201C;&#x7CFB;&#x7EDF;&#x201D;&#x4E8C;&#x8FDB;&#x5236;&#x6587;&#x4EF6;&#x3002;&#x5B83;&#x4EEC;&#x662F;&#x5B8C;&#x6210;&#x91CD;&#x5927;&#x7CFB;&#x7EDF;&#x4EFB;&#x52A1;&#x7684;&#x7A0B;&#x5E8F;&#xFF0C;&#x901A;&#x5E38;&#x4E3A;&#x8D85;&#x7EA7;&#x7528;&#x6237;&#x4FDD;&#x7559;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/tmp</td>
      <td style="text-align:left">&#x8FD9;&#x4E2A;/tmp &#x76EE;&#x5F55;&#xFF0C;&#x662F;&#x7528;&#x6765;&#x5B58;&#x50A8;&#x7531;&#x5404;&#x79CD;&#x7A0B;&#x5E8F;&#x521B;&#x5EFA;&#x7684;&#x4E34;&#x65F6;&#x6587;&#x4EF6;&#x7684;&#x5730;&#x65B9;&#x3002;&#x4E00;&#x4E9B;&#x914D;&#x7F6E;&#x5BFC;&#x81F4;&#x7CFB;&#x7EDF;&#x6BCF;&#x6B21;
        &#x91CD;&#x65B0;&#x542F;&#x52A8;&#x65F6;&#xFF0C;&#x90FD;&#x4F1A;&#x6E05;&#x7A7A;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr</td>
      <td style="text-align:left">&#x5728; Linux &#x7CFB;&#x7EDF;&#x4E2D;&#xFF0C;/usr &#x76EE;&#x5F55;&#x53EF;&#x80FD;&#x662F;&#x6700;&#x5927;&#x7684;&#x4E00;&#x4E2A;&#x3002;&#x5B83;&#x5305;&#x542B;&#x666E;&#x901A;&#x7528;&#x6237;&#x6240;&#x9700;&#x8981;&#x7684;&#x6240;&#x6709;&#x7A0B;&#x5E8F;&#x548C;&#x6587;&#x4EF6;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr/bin</td>
      <td style="text-align:left">/usr/bin &#x76EE;&#x5F55;&#x5305;&#x542B;&#x7CFB;&#x7EDF;&#x5B89;&#x88C5;&#x7684;&#x53EF;&#x6267;&#x884C;&#x7A0B;&#x5E8F;&#x3002;&#x901A;&#x5E38;&#xFF0C;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x4F1A;&#x5305;&#x542B;&#x8BB8;&#x591A;&#x7A0B;&#x5E8F;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr/lib</td>
      <td style="text-align:left">&#x5305;&#x542B;&#x7531;/usr/bin &#x76EE;&#x5F55;&#x4E2D;&#x7684;&#x7A0B;&#x5E8F;&#x6240;&#x7528;&#x7684;&#x5171;&#x4EAB;&#x5E93;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr/local</td>
      <td style="text-align:left">&#x8FD9;&#x4E2A;/usr/local &#x76EE;&#x5F55;&#xFF0C;&#x662F;&#x975E;&#x7CFB;&#x7EDF;&#x53D1;&#x884C;&#x7248;&#x81EA;&#x5E26;&#x7A0B;&#x5E8F;&#x7684;&#x5B89;&#x88C5;&#x76EE;&#x5F55;&#x3002;
        &#x901A;&#x5E38;&#xFF0C;&#x7531;&#x6E90;&#x7801;&#x7F16;&#x8BD1;&#x7684;&#x7A0B;&#x5E8F;&#x4F1A;&#x5B89;&#x88C5;&#x5728;/usr/local/bin
        &#x76EE;&#x5F55;&#x4E0B;&#x3002;&#x65B0;&#x5B89;&#x88C5;&#x7684; Linux
        &#x7CFB;&#x7EDF;&#x4E2D;&#x4F1A;&#x5B58;&#x5728;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#xFF0C;
        &#x5E76;&#x4E14;&#x5728;&#x7BA1;&#x7406;&#x5458;&#x5B89;&#x88C5;&#x7A0B;&#x5E8F;&#x4E4B;&#x524D;&#xFF0C;&#x8FD9;&#x4E2A;&#x76EE;&#x5F55;&#x662F;&#x7A7A;&#x7684;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr/sbin</td>
      <td style="text-align:left">&#x5305;&#x542B;&#x8BB8;&#x591A;&#x7CFB;&#x7EDF;&#x7BA1;&#x7406;&#x7A0B;&#x5E8F;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr/share</td>
      <td style="text-align:left">/usr/share &#x76EE;&#x5F55;&#x5305;&#x542B;&#x8BB8;&#x591A;&#x7531;/usr/bin
        &#x76EE;&#x5F55;&#x4E2D;&#x7684;&#x7A0B;&#x5E8F;&#x4F7F;&#x7528;&#x7684;&#x5171;&#x4EAB;&#x6570;&#x636E;&#x3002;
        &#x5176;&#x4E2D;&#x5305;&#x62EC;&#x50CF;&#x9ED8;&#x8BA4;&#x7684;&#x914D;&#x7F6E;&#x6587;&#x4EF6;&#x3001;&#x56FE;&#x6807;&#x3001;&#x684C;&#x9762;&#x80CC;&#x666F;&#x3001;&#x97F3;&#x9891;&#x6587;&#x4EF6;&#x7B49;&#x7B49;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/usr/share/doc</td>
      <td style="text-align:left">&#x5927;&#x591A;&#x6570;&#x5B89;&#x88C5;&#x5728;&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;&#x8F6F;&#x4EF6;&#x5305;&#x4F1A;&#x5305;&#x542B;&#x4E00;&#x4E9B;&#x6587;&#x6863;&#x3002;&#x5728;/usr/share/doc
        &#x76EE;&#x5F55;&#x4E0B;&#xFF0C; &#x6211;&#x4EEC;&#x53EF;&#x4EE5;&#x627E;&#x5230;&#x6309;&#x7167;&#x8F6F;&#x4EF6;&#x5305;&#x5206;&#x7C7B;&#x7684;&#x6587;&#x6863;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/var</td>
      <td style="text-align:left">&#x9664;&#x4E86;/tmp &#x548C;/home &#x76EE;&#x5F55;&#x4E4B;&#x5916;&#xFF0C;&#x76F8;&#x5BF9;&#x6765;&#x8BF4;&#xFF0C;&#x76EE;&#x524D;&#x6211;&#x4EEC;&#x770B;&#x5230;&#x7684;&#x76EE;&#x5F55;&#x662F;&#x9759;&#x6001;&#x7684;&#xFF0C;&#x8FD9;&#x662F;&#x8BF4;&#xFF0C;
        &#x5B83;&#x4EEC;&#x7684;&#x5185;&#x5BB9;&#x4E0D;&#x4F1A;&#x6539;&#x53D8;&#x3002;/var
        &#x76EE;&#x5F55;&#x5B58;&#x653E;&#x7684;&#x662F;&#x52A8;&#x6001;&#x6587;&#x4EF6;&#x3002;&#x5404;&#x79CD;&#x6570;&#x636E;&#x5E93;&#xFF0C;&#x5047;&#x8131;&#x673A;&#x6587;&#x4EF6;&#xFF0C;
        &#x7528;&#x6237;&#x90AE;&#x4EF6;&#x7B49;&#x7B49;&#xFF0C;&#x90FD;&#x4F4D;&#x4E8E;&#x5728;&#x8FD9;&#x91CC;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">/var/log</td>
      <td style="text-align:left">&#x8FD9;&#x4E2A;/var/log &#x76EE;&#x5F55;&#x5305;&#x542B;&#x65E5;&#x5FD7;&#x6587;&#x4EF6;&#x3001;&#x5404;&#x79CD;&#x7CFB;&#x7EDF;&#x6D3B;&#x52A8;&#x7684;&#x8BB0;&#x5F55;&#x3002;&#x8FD9;&#x4E9B;&#x6587;&#x4EF6;&#x975E;&#x5E38;&#x91CD;&#x8981;&#xFF0C;&#x5E76;&#x4E14;
        &#x5E94;&#x8BE5;&#x65F6;&#x65F6;&#x76D1;&#x6D4B;&#x5B83;&#x4EEC;&#x3002;&#x5176;&#x4E2D;&#x6700;&#x91CD;&#x8981;&#x7684;&#x4E00;&#x4E2A;&#x6587;&#x4EF6;&#x662F;/var/log/messages&#x3002;&#x6CE8;&#x610F;&#xFF0C;&#x4E3A;&#x4E86;&#x7CFB;&#x7EDF;&#x5B89;&#x5168;&#xFF0C;&#x5728;&#x4E00;&#x4E9B;&#x7CFB;&#x7EDF;&#x4E2D;&#xFF0C;
        &#x4F60;&#x5FC5;&#x987B;&#x662F;&#x8D85;&#x7EA7;&#x7528;&#x6237;&#x624D;&#x80FD;&#x67E5;&#x770B;&#x8FD9;&#x4E9B;&#x65E5;&#x5FD7;&#x6587;&#x4EF6;&#x3002;</td>
    </tr>
  </tbody>
</table>#### 硬链接/软链接\(符号链接\)

{% embed url="https://blog.csdn.net/geerniya/article/details/79093301" %}

{% embed url="https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/index.html" %}















{% embed url="https://i.linuxtoy.org/files/pdf/fwunixref.pdf" %}

{% file src="../../.gitbook/assets/unix-comment-cheat-sheet.pdf" caption="Unix/Linux comment cheat sheet" %}

{% embed url="http://billie66.github.io/TLCL/book/chap01.html" %}




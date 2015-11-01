世界上有三中程序员，一种是用 Vim 的，一种是用 Emacs 的，另外一种是用其它编辑器的。本文介绍 Emacs 的基本使用。

# 一、Emacs24 的安装

    wget https://github.com/mirrors/emacs/archive/emacs-24.3.92.zip
    unzip emacs-24.3.92.zip
    cd emacs-24.3.93
    ./autogen.sh
    ./configure --without-makeinfo
    make -j2
    sudo make install
    
添加 `alias em='env TERM=xterm-256color emacs -nw` 到 `~/.bashrc` 中，这样就可以直接用 `em` 打开 Emacs 了。

# 二、基本快捷键

这里列出在没有打开任何 mode 的情况下，原生 Emacs 所支持的快捷键。

+ `C-`: Ctrl 键
+ `M-`: Alt/ESC 键,
+ `S-`: Shift 键
+ `C-g` : 撤销命令(没事多摁几下，我都是没事摁着玩的)
+ `C-z` : 挂起 Emacs
+ `C-x C-c`: 关闭 Emacs

## 2.1 光标移动

+ `C-n` : 下一行
+ `C-p` : 上一行
+ `C-f` : 前进一个字符
+ `C-b` : 后退一个字符
+ `M-f` : 前进一个单词
+ `M-b` : 后退一个单词
+ `C-v` : 向下翻页
+ `M-v` : 向上翻页
+ `C-l` : 光标所在行移动到屏幕中央
+ `C-a` : 行首
+ `C-e` : 行尾
+ `M-a` : 句首
+ `M-e` : 句尾
+ `M-<` : 文件首
+ `M->` : 文件尾

## 2.2 文档编辑

+ `<Backspace>` : 向前删除一个字符
+ `C-d` `<DEL>` : 向后删除一个字符，我一般用 `C-d`
+ `M-d` `M-<DEL>` : 向后删除一个单词
+ `C-k` : 删除光标到行尾，删除一行用 `C-a, C-k` (Vim 中的 dd)。
+ `M-k` : 删除光标到句尾
+ `C-@` : 标记(Mark set), 标记之后配合光标移动快捷键，可以选中一个区域
+ `M-w` : 复制
+ `C-w` : 剪切
+ `C-y` : 粘贴
+ `C-/` : 撤销(UNDO)

大小写转换:

+ `M-l`: Convert following word to lower case (downcase-word).
+ `M-u`: Convert following word to upper case (upcase-word).
+ `M-c`: Capitalize the following word (capital-word).
+ `C-x C-l`: Convert region to lower case (downcase-region).
+ `C-x C-u`: Convert region to upper case (upcase-region).

块操作:

+ `C-x r k`: Kill the text of the region-rectangle, saving its contents as the “last killed rectangle” (kill-rectangle).
+ `C-x r M-w`: Save the text of the region-rectangle as the “last killed rectangle” (copy-rectangle-as-kill).
+ `C-x r d`: Delete the text of the region-rectangle (delete-rectangle).
+ `C-x r y`: Yank the last killed rectangle with its upper left corner at point (yank-rectangle).
+ `C-x r o`: Insert blank space to fill the space of the region-rectangle (open-rectangle). This pushes the previous contents of the region-rectangle to the right.
+ `C-x r N`: Insert line numbers along the left edge of the region-rectangle (rectangle-number-lines). This pushes the previous contents of the region-rectangle to the right.
+ `C-x r c`: Clear the region-rectangle by replacing all of its contents with spaces (clear-rectangle).
+ `M-x delete-whitespace-rectangle`: Delete whitespace in each of the lines on the specified rectangle, starting from the left edge column of the rectangle.
+ `C-x r t string <RET>`: Replace rectangle contents with string on each line (string-rectangle).
+ `M-x string-insert-rectangle <RET> string <RET>`: Insert string on each line of the rectangle.


## 2.3 搜索

+ `C-s` : 向前搜索
+ `C-r` : 向后操作
+ `C-g` : 回到搜索开始前的位置
+ `M-%` : 询问并替换

## 2.4 文件操作(缓冲区)

Emacs 可以打开很多文件，一个文件可以理解成一个 buffer，你可以在多个文件中来回切换。

+ `C-x f` : 打开一个文件 -> `find-file`
+ `C-x s` : 保存
+ `C-x C-w` : 另存为
+ `C-x C-v` : 关闭当前缓冲区，并打开新文件
+ `C-x C-b` : 打开缓冲区列表
+ `C-x b` : 切回最近的 buffer -> `switch-to-buffer`
+ `C-x k` : 关闭当前缓冲区
+ `C-x C-b`, `d`, `x`: 关闭用 d 标记 buffer
+ `M-x find-file-at-point` , `M-x ffap`
+ `C-x 5 0` : `delete-frame`

## 2.5 窗口(WINDOWS)操作

+ `C-x 1` : 只保留当前窗口
+ `C-x 2` : 水平切分
+ `C-x 3` : 垂直切分
+ `C-x o` : 切换到另外一个窗口
+ `C-x 0` : 关闭当前窗口(并不是删除buffer)
+ `C-x 4 C-f` : 在另外一个窗口打开文件 -> `find-file-other-window`

## 2.6 查阅命令

+ `M-x man` :
+ `M-x info` : 所有的 Emacs 手册

## 2.7 代码编辑

+ `M-;` : 块注释

## 2.8 目录操作

+ `M-x dired` : 打开一个目录

## 2.9 书签

+ `C-x r m` : 设置一个书签 -> `bookmark-set`
+ `C-x r b` : 跳转到一个书签 -> `bookmark-jump`
+ `C-x r l` : 显示所有书签列表, 管理书签的方式和 `Direcd` 模式一样
	- `RET` : 打开一个书签
	- `p`: 前一个书签
	- `n`: 后一个书签
	- `s` : 保存当前书签到一个文件中
	- `o` : 在另外一个窗口中打开文件
	- `r` : 重命名书签
	- `d` : 标记要删除的书签
	- `x` : 执行删除动作
	- `u` : 撤销标记

## 2.10 Occur

把所有的搜索结果都列到一个名为 `*Occur*` buffer 中。使用 `M-s o` 调用 `occur` 函数，搜索当前文档。

+ `M-g n` : 下一个匹配项
+ `M-g p` : 上一个匹配项
+ `e` : 进入 `occur-edit-mode`，可以编辑搜索结果
+ `C-c C-c` : 退出编辑模式
+ `g` : 刷新搜索结果

## 2.11 Dired

+ `C-x d` : 选个一个目录，在当前窗口打开
+ `C-x 4 d` : 选一个目录，在另外一个目录打开
+ `i` : 打开子目录

## 2.12 版本控制(Version Control)

+ `C-x v v` , `M-x vc-next-action` : 提交当前文件
+ `C-x v =` , `M-x vc-diff`
+ `C-x v ~` , `M-x vc-revision-other-window`: 与指定版本做比较
+ `C-x v l` , `M-x vc-print-log` : 查看日志
+ `C-x v u` , `M-x vc-revert` 
+ `C-x v C-h` : 查看所有可用的 vc 命令

# 三、通用定制

默认的 emacs 的快捷键有些不好用，比如 `c-x c-f` 时，没有任何提示。再如窗口切换使用 `c-x o`，当 buffer 多时，非常不方便，这一节介绍 emacs 通用的定制(不针对某种开发/编辑环境)。

emacs 的配置文件为 `~/.emacs`，如果没有就 `touch` 一个，插件位置一般在 `~/.emacs.d`，如果没有就 `mkdir` 一个。Emacs 启动时会加载这些配置(也因此会减慢Emacs的启动速度，建议不要给Emacs装太多的插件，看着花哨但不实用)。

用 `y/n` 代替 `yes/no`:

    (fset 'yes-or-no-p 'y-or-n-p)

设置编码为 UTF-8

    (setq locale-coding-system 'utf-8)
    (set-terminal-coding-system 'utf-8)
    (set-keyboard-coding-system 'utf-8)
    (set-selection-coding-system 'utf-8)
    (prefer-coding-system 'utf-8)

`C-c e` 打开 eshell, `C-c l`清空 eshell:

    (defun clear-eshell-buffer ()
      (interactive)
      (let ((inhibit-read-only t))
        (delete-region (point-min) (point-max))))
    (global-set-key (kbd "C-c l") 'clear-eshell-buffer)
    (global-set-key (kbd "C-c e") 'eshell)

tab -> 空格:

    (setq-default indent-tabs-mode nil)

括号匹配、对齐、补全：

    (show-paren-mode t)
    (require 'electric)
    (electric-indent-mode t)
    (electric-pair-mode t)
    (electric-layout-mode t)
    

保存时删除多余的空白字符:
    
    (add-hook 'before-save-hook 'delete-trailing-whitespace)
    (setq show-trailing-whitespace t)

去掉自动保存和备份:

    (setq auto-save-default nil)
    (setq make-backup-files nil)


行号:

    (setq linum-format "%3d|")
    (global-linum-mode 1)

自动换行：

    (global-visual-line-mode 1)
    (blink-cursor-mode -1)

使用 M-(1,2,3...9)窗口切换(依赖于 windows-numbering 插件):

    (add-to-list 'load-path "~/.emacs.d/lisp/window-numbering.el")
    (require 'window-numbering)
    (setq window-numbering-assign-func
          (lambda () (when (equal (buffer-name) "*Calculator*") 9)))
    (window-numbering-mode 1)

Mini Buffer 优化(依赖 smex 插件，ido 是 Emacs 自带的):

    ;; C-x f/b
    (require 'ido)
    (ido-mode t)
    ;; M-x
    (add-to-list 'load-path "~/.emacs.d/lisp/smex")
    (require 'smex)
    (smex-initialize)
    (global-set-key (kbd "M-x") 'smex)
    (global-set-key (kbd "M-X") 'smex-major-mode-commands)

使用 `ibuffer` 代替默认的 `list-buffers`:

    (global-set-key (kbd "C-x C-b") 'ibuffer)

`C-a` 跳转到句首，而不是行首:

    (defun prelude-move-beginning-of-line (arg)
      "Move point back to indentation of beginning of line.
    
    Move point to the first non-whitespace character on this line.
    If point is already there, move to the beginning of the line.
    Effectively toggle between the first non-whitespace character and
    the beginning of the line.
    
    If ARG is not nil or 1, move forward ARG - 1 lines first. If
    point reaches the beginning or end of the buffer, stop there."
      (interactive "^p")
      (setq arg (or arg 1))
    
      ;; Move lines first
      (when (/= arg 1)
        (let ((line-move-visual nil))
          (forward-line (1- arg))))
    
      (let ((orig-point (point)))
        (back-to-indentation)
        (when (= orig-point (point))
          (move-beginning-of-line 1))))
    
    (global-set-key (kbd "C-a") 'prelude-move-beginning-of-line)

Tip:  `M-x eval-buffer` 可以使配置文件立即生效，调试非常方便。

# 四、高级定制

这一节针对不同的应用，介绍一些插件。

## 4.1 代码参考线: [fill-column-indicator](https://github.com/alpaker/Fill-Column-Indicator)

    (require 'fill-column-indicator)
    (setq fci-rule-color "#333") # 参考线颜色，我的配色是暗色的, 所以 #333 看着舒服一点
    (setq fci-rule-column 80)    # 宽度设置为 80 
    (define-globalized-minor-mode
      global-fci-mode fci-mode (lambda () (fci-mode 1)))
    (global-fci-mode 1)

## 4.2 自动补全:

### 4.2.1 [auto-complete](https://github.com/auto-complete/auto-complete)

    (require 'popup)
    (require 'auto-complete-config)
    (add-to-list 'ac-dictionary-directories
                 "~/.emacs.d/auto-complete/dict")
    (ac-config-default)
    (setq ac-use-quick-help nil)
    (setq ac-ignore-case t)
    (setq ac-menu-height 8)
    
    (setq ac-use-menu-map t)
    (define-key ac-menu-map "\C-n" 'ac-next)
    (define-key ac-menu-map "\C-p" 'ac-previous)
    (global-set-key "\M-/" 'auto-complete)

### 4.2.2 [Company mode](http://www.emacswiki.org/CompanyMode)

### 4.2.3 [yasnippet](https://github.com/capitaomorte/yasnippet)

## 4.3 相同符号高亮: [highlight-symbol](https://github.com/nschum/highlight-symbol.el)

用这个做查找也挺不错的!

    (require 'highlight-symbol)
    (global-set-key (kbd "M--") 'highlight-symbol-at-point)
    (global-set-key (kbd "M-n") 'highlight-symbol-next)
    (global-set-key (kbd "M-p") 'highlight-symbol-prev)

## 4.4 Markdown: [markdown-mode](http://jblevins.org/projects/markdown-mode/)

    (autoload 'markdown-mode "~/.emacs.d/lisp/markdown-mode/markdown-mode.el"
      "Major mode for editing Markdown files" t)
    (setq auto-mode-alist
          (cons '("\\.md" . markdown-mode) auto-mode-alist))
    (setq auto-mode-alist
          (cons '("\\.markdown" . markdown-mode) auto-mode-alist))
    (setq auto-mode-alist
          (cons '("\\.txt" . markdown-mode) auto-mode-alist))

## 4.5 Python: [python.el](https://github.com/fgallina/python.el)

推荐使用 python.el 而不是 [python-mode](https://github.com/klen/python-mode)。

    (require 'python)

## 4.6 Google Protobuf Buffer: [protobuf-mode](http://code.google.com/p/protobuf/source/browse/trunk/editors/protobuf-mode.el?r=227)

    (require 'protobuf-mode)
    (add-to-list 'auto-mode-alist '("\\.proto$" . protobuf-mode))

## 4.7 C++开发定制: xcscope + etags + c++-mode

    ;; 编译与调试
    (global-set-key [(f5)] 'compile)
    
    (require 'xcscope)
    (cscope-setup)
    
    (global-set-key [(f9)] 'ff-find-other-file)
    
    (setq tab-stop-list ())
    (loop for x downfrom 40 to 1 do
          (setq tab-stop-list (cons (* x 4) tab-stop-list)))
    
    (defconst my-c-style
      '(
        (c-tab-always-indent        . t)
        (c-hanging-braces-alist     . ((substatement-open after)
                                       (brace-list-open)))
        (c-hanging-colons-alist     . ((member-init-intro before)
                                       (inher-intro)'
                                       (label after)
                                       (acecss-label after)))
        (c-cleanup-list             . (scope-operator
                                       empty-defun-braces
                                       defun-close-semi))
        (c-offsets-alist            . ((arglist-close . c-lineup-arglist)
                                       (case-label . 4)
                                       (substatement-open . 0)
                                       (block-open        . 0)
                                       (knr-argdecl-intro . -)
                                       (innamespace . -)
                                       (inline-open . 0)
                                       (inher-cont . c-lineup-multi-inher)
                                       (arglist-cont-nonempty . +)
                                       (template-args-cont . + )))
        (c-echo-syntactic-information-p . t)
        )
      "My C Programming Style")
    
    ;; offset customizations not in my-c-style
    (setq c-offsets-alist '((member-init-intro . ++)))
    
    ;; Customizations for all modes in CC Mode.
    (defun my-c-mode-common-hook ()
      ;; add my personal style and set it for the current buffer
      (c-add-style "PERSONAL" my-c-style t)
      ;; other customizations
      (setq tab-width 4
            indent-tabs-mode nil)
      ;; we like auto-newline and hungry-delete
      ;; (c-toggle-auto-hungry-state 1)
      ;; key bindings for all supported languages.  We can put these in
      ;; c-mode-base-map because c-mode-map, c++-mode-map, objc-mode-map,
      ;; java-mode-map, idl-mode-map, and pike-mode-map inherit from it.
      )
    (add-hook 'c-mode-common-hook 'my-c-mode-common-hook)
    (add-hook 'c-mode-hook 'hs-minor-mode)
    
    (add-to-list 'auto-mode-alist '("\\.h\\'" . c++-mode))
    
    ;; http://stackoverflow.com/questions/14668744/emacs-indent-for-c-class-method
    (defun vlad-cc-style()
      (c-set-offset 'inline-open '0)
      )
    (add-hook 'c++-mode-hook 'vlad-cc-style)

[xcscope.el](https://github.com/dkogan/xcscope.el) 使用:

+ cscope -r : 在根目录下递归生成数据库
+ C-c s a : Set initial directory;
+ C-c s A : Unset initial directory;
+ C-c s I : create list of files to index;
+ C-c s s : Find symbol;
+ C-c s d : Find global definition;
+ C-c s c : Find functions calling a function;
+ C-c s C : Find called functions (list functions called from a function);
+ C-c s t : Find text string;
+ C-c s e : Find egrep pattern;
+ C-c s f : Find a file;
+ C-c s i : Find files #including a file;
+ C-c s b : Display cscope buffer;

etags 使用:

搭配 `find` 来生成 tags:

    find . -name '*.c' -o -name '*.cpp' -o -name '*.h' -print | etags -

+ `M-x visit-tags-table <RET> FILE <RET>` : 选择tags文件
+ `M-. [TAG] <RET>` : 访问标签
+ `M-*` : 返回
+ `C-u M-.` : 寻找标签的下一个定义

其它：

+ `F9` : 在头文件和对应源文件之间跳转: `(global-set-key [(f9)] 'ff-find-other-file)`

## 4.8 [谷歌翻译](https://github.com/atykhonov/google-translate.git)


    (add-to-list 'load-path "~/.emacs.d/lisp/google-translate")
    (require 'google-translate)
    (require 'google-translate-smooth-ui)
    (global-set-key "\C-ct" 'google-translate-smooth-translate)
    (setq google-translate-translation-directions-alist
          '(("en" . "zh-CN") ("zh-CN" . "en") ))

`C-c t` 打开翻译，我指定了英->中，中->英两种翻译模式。

## 4.9 Expand region

Github: [expand-region.el](https://github.com/magnars/expand-region.el)

    (require 'expand-region)
    (global-set-key (kbd "M-m") 'er/expand-region)


## 4.10 Helm ()

github: [https://github.com/emacs-helm/helm](https://github.com/emacs-helm/helm)

**极力推荐** 这个插件，对于 Emacs 的基本使用是一个质的提升。安装了 helm 你会发现 ido, smex 神马的简直弱爆了。

推荐阅读: [helm-intro](http://tuhdo.github.io/helm-intro.html) 

    (add-to-list 'load-path "~/.emacs.d/lisp/helm")
    (require 'helm)
    
    (setq helm-command-prefix-key "C-c h")
    
    (require 'helm-config)
    (require 'helm-eshell)
    (require 'helm-files)
    (require 'helm-grep)
    
    (define-key helm-map (kbd "<tab>") 'helm-execute-persistent-action) ; rebind tab to do persistent action
    (define-key helm-map (kbd "C-i") 'helm-execute-persistent-action) ; make TAB works in terminal
    (define-key helm-map (kbd "C-z")  'helm-select-action) ; list actions using C-z
    
    (define-key helm-grep-mode-map (kbd "<return>")  'helm-grep-mode-jump-other-window)
    (define-key helm-grep-mode-map (kbd "n")  'helm-grep-mode-jump-other-window-forward)
    (define-key helm-grep-mode-map (kbd "p")  'helm-grep-mode-jump-other-window-backward)
    
    (setq
     helm-google-suggest-use-curl-p t
     helm-scroll-amount 4 ; scroll 4 lines other window using M-<next>/M-<prior>
     helm-quick-update t ; do not display invisible candidates
     helm-idle-delay 0.01 ; be idle for this many seconds, before updating in delayed sources.
     helm-input-idle-delay 0.01 ; be idle for this many seconds, before updating candidate buffer
     helm-ff-search-library-in-sexp t ; search for library in `require' and `declare-function' sexp.
    
     helm-split-window-default-side 'other ;; open helm buffer in another window
     helm-split-window-in-side-p t ;; open helm buffer inside current window, not occupy whole other window
     helm-buffers-favorite-modes (append helm-buffers-favorite-modes
                                         '(picture-mode artist-mode))
     helm-candidate-number-limit 200 ; limit the number of displayed canidates
     helm-M-x-requires-pattern 0     ; show all candidates when set to 0
     helm-boring-file-regexp-list
     '("\\.git$" "\\.hg$" "\\.svn$" "\\.CVS$" "\\._darcs$" "\\.la$" "\\.o$" "\\.i$") ; do not show these files in helm buffer
     helm-ff-file-name-history-use-recentf t
     helm-move-to-line-cycle-in-source t ; move to end or beginning of source
                                            ; when reaching top or bottom of source.
     ido-use-virtual-buffers t      ; Needed in helm-buffers-list
     helm-buffers-fuzzy-matching t          ; fuzzy matching buffer names when non--nil
                                            ; useful in helm-mini that lists buffers
     )
    
    ;; Save current position to mark ring when jumping to a different place
    (add-hook 'helm-goto-line-before-hook 'helm-save-current-pos-to-mark-ring)
    (helm-mode 1)
    
    (global-set-key (kbd "M-x") 'helm-M-x)
    (global-set-key (kbd "C-x b") 'helm-mini)
    (global-set-key (kbd "C-x C-f") 'helm-find-files)
    (global-set-key (kbd "C-c h o") 'helm-occur)
    (global-set-key (kbd "M-y") 'helm-show-kill-ring)
    
    (require 'helm-eshell)
    (add-hook 'eshell-mode-hook
              #'(lambda ()
                  (define-key eshell-mode-map (kbd "M-l")  'helm-eshell-history)))
    
    ;; C-c h / helm-find
    ;; C-c h m man or woman

## 4.last Emacs主题

把 主题 放到最后，是想告诉大家，使用 Emacs(或者其它任何工具) 时，不要花时间在这些炫酷的东西上面，还是要聚焦于实用和高效。Emacs24自带了几款主题(Emacs23没有的哦)，使用 `M-x customize-theme` 回车可查看配色效果。

也可以在学习资源中的 Emacs Theme 中找一款自己喜欢的。

# 五、学习资源 

一些学习资源推荐，也是本文档的参考资料。

+ [Emacs Mini Mannual](http://tuhdo.github.io/index.html) : Emacs Mini 手册
+ [Emacs Themes](http://emacsthemes.caisah.info/) : 主题集合
+ [MELPA](http://melpa.milkbox.net/) : 插件集合，同时也可以感受一下 Emacs 的强大
+ [GNU Emacs Manuals Online](http://www.gnu.org/software/emacs/manual/) : Emacs 官方手册
+ [Emacs Redux](http://emacsredux.com/)
+ [Emacs Markdown Mode](http://jblevins.org/projects/markdown-mode/)
+ [一年成为Emacs高手(像神一样使用编辑器)](https://github.com/redguardtoo/mastering-emacs-in-one-year-guide/blob/master/guide-zh.org)
+ [Emacs as a Python IDE](http://www.jesshamrick.com/2012/09/18/emacs-as-a-python-ide/)
+ [Emacs快速参考](http://jianlee.ylinux.org/Computer/Emacs/emacsBFE99F8FE883.html)
+ [Case Conversion Commands](http://www.gnu.org/software/emacs/manual/html_node/emacs/Case.html)
+ [曹乐: 在Emacs下用C/C++编程](http://www.caole.net/diary/emacs_write_cpp.html)


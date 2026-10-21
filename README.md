# LaTeX 论文编写框架模板

这是一个与具体会议或期刊无关的论文工程模板，适合从研究构思写到投稿前整理。入口文件是 `main.tex`，正文按章节拆分到 `sections/`，补充材料放在 `appendix/`。

## 目录结构

```text
latexTemplate/
├── main.tex                         # 编译入口、标题、作者和章节顺序
├── preamble.tex                     # 宏包、版式、定理环境和常用命令
├── references.bib                   # BibTeX 参考文献
├── sections/
│   ├── 01_introduction.tex          # 问题、动机和贡献
│   ├── 02_related_work.tex          # 相关工作和研究定位
│   ├── 03_method.tex                # 问题定义、方法和算法
│   ├── 04_experiments.tex           # 实验设置
│   ├── 05_results_and_discussion.tex# 结果、分析和局限
│   └── 06_conclusion.tex            # 结论和未来工作
├── appendix/
│   ├── appendix_a_additional_details.tex
│   └── appendix_b_additional_results.tex
├── figures/                         # 图片资源（建议 PDF/SVG 转 PDF）
└── tables/                          # 可复用的独立表格文件
```

## 快速开始

在 `latexTemplate/` 目录执行：

```bash
latexmk -xelatex -interaction=nonstopmode -halt-on-error main.tex
```

模板包含中文写作提示，建议直接使用 XeLaTeX。完成英文稿并删除中文提示后，也可以改用 `pdflatex`。清理辅助文件：

```bash
latexmk -C
```

## 推荐写作顺序

1. 先在 `main.tex` 填写标题、作者和关键词。
2. 在引言中先写清楚问题、研究缺口和三条以内的可验证贡献。
3. 再写方法和实验设置，确保每个主张都有对应的定义、算法、图或表。
4. 最后整理结果、局限、结论和摘要。
5. 提交前删除或重定义 `\placeholder{...}` 生成的 TODO 标记，并检查引用、图表、附录和复现实验信息。

## 常用写法

```latex
% 叙述式 / 括号式引用
\citet{vaswani2017attention}
\citep{devlin2019bert}

% 公式和交叉引用
\begin{equation}
  y = f_\theta(x)
  \label{eq:example}
\end{equation}
如 \cref{eq:example} 所示。

% 图片（把文件放入 figures/）
\begin{figure}[t]
  \centering
  \includegraphics[width=0.9\linewidth]{figures/example.pdf}
  \caption{图片说明。}
  \label{fig:example}
\end{figure}

% 表格：优先使用 booktabs，不使用竖线
\begin{table}[t]
  \centering
  \caption{表格说明。}
  \label{tab:example}
  \begin{tabular}{lcc}
    \toprule
    Method & Score $\uparrow$ & Time $\downarrow$ \\
    \midrule
    A & 0.00 & 0.00 \\
    \bottomrule
  \end{tabular}
\end{table}
```

投稿到特定会议或期刊时，把 `main.tex` 的 `\documentclass`、版式和参考文献样式替换为官方模板，并尽量保留章节文件的拆分方式。

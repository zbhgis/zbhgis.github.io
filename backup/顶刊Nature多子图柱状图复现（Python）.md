

## 结果对比

本文复现的这张图是2021年发表在Nature中的一张多子图柱状图。完整代码获取方法在文末。

论文原图：

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512101613789.png)

复现结果：

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512101613246.jpeg)

## 绘制思路

之前在b站找教程的时候，看到这个图，顺手复现一下，b站有视频手把手教了怎么从零到一绘制。我是在b站视频的基础上，完善了一些细节，并将子图的绘制代码封装起来，方便之后同时绘制更多子图（比如8个，12个）。这篇期刊中还有其他的一些图，都比较简单，挺适合新手用来入门Python科研绘图的，之后有时间也会逐一复现的。

```Plain
https://www.bilibili.com/video/BV1CW4y1W7Cv
```

这个图的绘制比较简单，就是画出4个柱状图子图然后进一步拼接。

需要注意的就是第二个子图的图例是和另外三个相反的；

可能是因为图幅小，如果使用原生的x轴刻度线会有点越过坐标轴的感觉，因此还需要额外绘制x轴刻度线。

这次就直接通过肉眼识别把柱状图的高度提取出来，作为代码的输入数据。

主要代码如下：

```Python
"""
Author: https://github.com/zbhgis
Paper source: https://doi.org/10.1038/s41586-021-03344-2
Paper Figure source: https://www.nature.com/articles/s41586-021-03344-2/figures/6
Last Modified: 2025-12-05
Data: The data used in the code is obtained by visual recognition
"""

import numpy as np
import matplotlib.pyplot as plt
import utils

# 绘图函数
def create_bar_plot(
    ax,
    bar_data=[
        [0.45, 0.16, 0.11, 0.15, 0.10, 0.08],
        [0.55, 0.17, 0.08, 0.13, 0.07, 0.06],
    ],
    bar_label=["Control", "Treatment"],
    bar_color=["#D82E18", "#5DB1DE"],
    bar_width=0.25,
    capsize=3,
    title="Study 3\nFalse Headline",
    x_label="Sharing Likelyhood",
    y_label="Frequency",
    x_tick_label=[
        "Extremely\nunlikely",
        "Moderately\nunlikely",
        "Slightly\nunlikely",
        "Slightly\nlikely",
        "Moderately\nlikely",
        "Extremely\nlikely",
    ],
    y_tick_label=np.arange(0, 0.7, 0.1),
):
    # 画图
    x = np.arange(len(bar_data[0]))
    # 绘制子图中的每个柱状图
    for i in range(0, len(bar_data)):
        offset = bar_width * (i - (len(bar_data) - 1) / 2)
        ax.bar(
            x + offset,
            bar_data[i],
            width=bar_width,
            label=bar_label[i],
            color=bar_color[i],
            capsize=capsize,
        )

    # 添加标题和轴标签
    ax.set_title(title)
    ax.set_xlabel(x_label)
    ax.set_ylabel(y_label)

    # 隐藏顶部和右侧的轴线
    ax.spines["top"].set_visible(False)
    ax.spines["right"].set_visible(False)

    # 设置x轴
    ax.set_xticks(x, x_tick_label)
    # 添加新的x轴刻度线
    utils.add_ticks(
        ax, axis="x", num_ticks=len(bar_data[0]) + 1, ymin=-0.01, ymax=-0.005
    )

    # 设置y轴
    ax.set_yticks(y_tick_label)
    ax.tick_params(axis="y", which="both", length=0)

    # 刻度保留两位小数
    utils.format_ticks(ax, y_zero_format=True, y_precision=2)

    # 绘制图例
    ax.legend(frameon=False)

if __name__ == "__main__":
    # 统一绘图样式
    plt.rcdefaults()
    plt.rcParams.update(
        {
            "font.family": "Times New Roman",  # 字体
            "axes.titlesize": 20,  # 子图标题大小
            "axes.labelsize": 16,  # 坐标轴标签大小
            "xtick.labelsize": 8,  # x轴刻度标签大小
            "ytick.labelsize": 14,  # y轴刻度标签大小
            "legend.fontsize": 15,  # 图例字体大小
            "axes.linewidth": 1,  # 坐标轴线宽
            "lines.linewidth": 1,  # 线宽
            "legend.handlelength": 0.6,  # 图例长度
            "legend.handleheight": 0.6,  # 图例高度
            "legend.handletextpad": 0.3,  # 图例与图例文字距离
        }
    )

    # 条形图数据
    bar_data_list = [
        [[0.45, 0.16, 0.11, 0.15, 0.10, 0.08], [0.55, 0.17, 0.08, 0.13, 0.07, 0.06]],
        [[0.33, 0.18, 0.16, 0.17, 0.12, 0.08], [0.32, 0.20, 0.14, 0.19, 0.15, 0.06]],
        [[0.46, 0.13, 0.09, 0.135, 0.1, 0.12], [0.53, 0.125, 0.085, 0.125, 0.09, 0.09]],
        [[0.3, 0.19, 0.17, 0.186, 0.12, 0.08], [0.33, 0.17, 0.16, 0.196, 0.128, 0.086]],
    ]

    # 条形图标签
    bar_label_strs = ["Control", "Treatment"]

    # 条形图颜色
    bar_color_list = [
        ["#D82E18", "#5DB1DE"],
        ["#5DB1DE", "#D82E18"],
        ["#D82E18", "#5DB1DE"],
        ["#D82E18", "#5DB1DE"],
    ]

    # 标题
    title_list = [
        "Study 3\nFalse Headline",
        "Study 3\nTrue Headline",
        "Study 4\nFalse Headline",
        "Study 4\nTrue Headline",
    ]

    # 标签文本
    x_label_str = "Sharing Likelyhood"
    y_label_str = "Frequency"

    # x轴刻度文本
    x_tick_label_strs = [
        "Extremely\nunlikely",
        "Moderately\nunlikely",
        "Slightly\nunlikely",
        "Slightly\nlikely",
        "Moderately\nlikely",
        "Extremely\nlikely",
    ]

    # y轴刻度数字
    y_tick_label_strs = np.arange(0, 0.7, 0.1)

    _, ax_list = utils.add_subplots(tw=10, th=10, wspace=0.3, hspace=0.5)

    # 创建子图
    for i in range(0, 4):
        create_bar_plot(
            ax_list[i],
            bar_data_list[i],
            bar_label_strs,
            bar_color_list[i],
            0.25,
            3,
            title_list[i],
            x_label_str,
            y_label_str,
            x_tick_label_strs,
            y_tick_label_strs,
        )

    # 导出为jpg文件，默认在当前路径下
    utils.export_fig()
    # 导出为指定路径下的指定文件名的tiff文件，dpi为500
    # utils.export_fig(
    #     formats="tiff", output_path=r"C:\Users\dell\Desktop\test.tiff", dpi=500
    # )

    # # 直接用plt.show()会导致比例失常，所以得看最终导出的图。
    # plt.show()
```

## 完整代码

github仓库链接

```Plain
https://github.com/zbhgis/QuickPlot
```

或者公众号后台回复 **图表复现**

在QuickPlot仓库 plot文件夹的bar文件夹下，过程中使用的其他封装工具函数在utils文件夹下。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512101613670.png)

## 参考

https://www.bilibili.com/video/BV1CW4y1W7Cv

https://www.nature.com/articles/s41586-021-03344-2/figures/6
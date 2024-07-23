- [【Qt开发教程】信号重定向QSignalMapper类详解及实战应用-CSDN博客](https://alextechvision.blog.csdn.net/article/details/140577357)
#### 
#### 实例
~~~c++
#include "mainwindow.h"
#include <QPushButton>
#include <QVBoxLayout>
#include <QMessageBox>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent), signalMapper(new QSignalMapper(this)) {

    QWidget *centralWidget = new QWidget(this);
    QVBoxLayout *layout = new QVBoxLayout;

    // 创建按钮并添加到布局中
    for (int i = 1; i <= 3; ++i) {
        QPushButton *button = new QPushButton("按钮 " + QString::number(i));
        layout->addWidget(button);
        
        // 将按钮的点击信号连接到 signalMapper 的 map() 槽
        connect(button, &QPushButton::clicked, signalMapper, qOverload<>(&QSignalMapper::map));
        // 设置信号映射
        signalMapper->setMapping(button, i);
    }
    
    // 连接 signalMapper 的 mapped(int) 信号到自定义槽函数
    connect(signalMapper, &QSignalMapper::mappedInt, this, &MainWindow::handleButtonPress);

    centralWidget->setLayout(layout);
    setCentralWidget(centralWidget);
}

MainWindow::~MainWindow() {}

void MainWindow::handleButtonPress(int id) {
    QMessageBox::information(this, "按钮按下", "按钮 " + QString::number(id) + " 被按下");
}
~~~

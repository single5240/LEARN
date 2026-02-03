```cpp
#include <QCoreApplication>
#include <QDebug>
#include <QFile>
#include <QStringList>
void readCsvFile(const QString &filePath) {
    QFile file(filePath);
    if (!file.open(QIODevice::ReadOnly | QIODevice::Text)) {
        qDebug() << "Failed to open the file.";
        return;
    }
    while (!file.atEnd()) {
        QByteArray line = file.readLine();
        QStringList fields = QString(line).split(",");
        qDebug() << fields;
    }
    file.close();
}
int main(int argc, char *argv[]) {
    QCoreApplication app(argc, argv);
    readCsvFile("example.csv");
    return app.exec();
}
```
- 将excel文件转换为csv文件
- 再读取csv文件
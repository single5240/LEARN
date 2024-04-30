## OTA升级流程
- 必须通过串行端口完成第一个固件上传
## API
### a.获得配置和启动程序的分区信息
1. 获取当前配置的启动应用程序的分区信息-`const esp_partition_t* esp_ota_get_boot_partition(void);`
2. 获取当前正在运行的应用程序的分区信息-`const esp_partition_t* esp_ota_get_running_partition(void);`
3. 返回下一个应使用新固件写入的OTA应用程序分区-`const esp_partition_t* esp_ota_get_next_update_partition(const esp_partition_t *start_from);`
### b.更新写入指定的分区
1. 开始OTA更新写入指定的分区-`esp_err_t esp_ota_begin(const esp_partition_t* partition, size_t image_size, esp_ota_handle_t* out_handle);`
### c.通过http将数据写入到分区中
1. 将OTA更新数据写入分区此功能可以多次调用-`esp_err_t esp_ota_write(esp_ota_handle_t handle, const void* data, size_t size);`
2. 完成OTA更新并验证新编写的应用程序映像-`esp_err_t esp_ota_end(esp_ota_handle_t handle);`
### d.重新设置分区
1. 为新的启动分区配置OTA数据-`esp_err_t esp_ota_set_boot_partition(const esp_partition_t* partition);`
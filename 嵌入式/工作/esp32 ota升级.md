## OTA升级流程
- 必须通过串行端口完成第一个固件上传
## API
### a.获得配置和启动程序的分区信息
1. `const esp_partition_t* esp_ota_get_boot_partition(void);`
2. `const esp_partition_t* esp_ota_get_running_partition(void);`
3. `const esp_partition_t* esp_ota_get_next_update_partition(const esp_partition_t *start_from);`
### b.更新写入指定的分区
1. `esp_err_t esp_ota_begin(const esp_partition_t* partition, size_t image_size, esp_ota_handle_t* out_handle);`
2. 
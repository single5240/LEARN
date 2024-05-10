## API
1. `nvs_flash_init` 初始化默认NVS分区
2.  `nvs_flash_erase` 擦除默认的NVS分区
3.  `nvs_open` 从默认NVS分区打开具有给定命名空间的非易失性存储
4.  读取函数
	```c
esp_err_t nvs_get_i8  (nvs_handle_t handle, const char* key, int8_t* out_value);
esp_err_t nvs_get_u8  (nvs_handle_t handle, const char* key, uint8_t* out_value);
esp_err_t nvs_get_i16 (nvs_handle_t handle, const char* key, int16_t* out_value);
esp_err_t nvs_get_u16 (nvs_handle_t handle, const char* key, uint16_t* out_value);
esp_err_t nvs_get_i32 (nvs_handle_t handle, const char* key, int32_t* out_value);
esp_err_t nvs_get_u32 (nvs_handle_t handle, const char* key, uint32_t* out_value);
esp_err_t nvs_get_i64 (nvs_handle_t handle, const char* key, int64_t* out_value);
esp_err_t nvs_get_u64 (nvs_handle_t handle, const char* key, uint64_t* out_value);
```




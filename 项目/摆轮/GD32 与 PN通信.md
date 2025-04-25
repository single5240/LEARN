### GD32 ---> PN
```c
	pn_send_data.real.head0 = PN_DATA_HEAD;
    pn_send_data.real.data_len = len;
    pn_send_data.real.head1 = PN_DATA_HEAD;
    memcpy(&pn_send_data.real.out_data, data, len);
    pn_send_data.raw[3+len] = PN_DATA_END;
```

### PN ---> GD32
```c
	pn_send_data.real.head0 = PN_DATA_HEAD;
    pn_send_data.real.data_len = len;
    pn_send_data.real.head1 = PN_DATA_HEAD;
    memcpy(&pn_send_data.real.out_data, data, len);
    pn_send_data.raw[3+len] = PN_DATA_END;
```


# VESC驱动
## 代码组成
1. VESC_Driver.c
2. VESC_Driver.h
3. WTRconfig.h

## 使用方法
调用函数`HAL_StatusTypeDef can_send_command(VESC_t *hvesc, const CAN_PACKET_MODE_ID id, float value,int all);`来发送控制指令。

下面与各部分参数设置有关：

### 1 VESC_t *hvesc

```c
typedef struct{
#ifdef __VESC_CAN_ENABLE	
	CAN_HandleTypeDef * hcann;
	uint8_t controller_id;
#endif
#ifdef __VESC_UART_ENABLE
	UART_HandleTypeDef * huartn;
	
#endif
}VESC_t;
```

### 2 const  CAN_PACKET_MODE_ID id

```c
#ifdef __VESC_CAN_ENABLE
typedef enum {
	CAN_PACKET_SET_DUTY = 0,
	CAN_PACKET_SET_CURRENT,
	CAN_PACKET_SET_CURRENT_BRAKE,
	CAN_PACKET_SET_RPM,
	CAN_PACKET_SET_POS,
	CAN_PACKET_FILL_RX_BUFFER,
	CAN_PACKET_FILL_RX_BUFFER_LONG,
	CAN_PACKET_PROCESS_RX_BUFFER,
	CAN_PACKET_PROCESS_SHORT_BUFFER,
	CAN_PACKET_STATUS,
	CAN_PACKET_SET_CURRENT_REL,
	CAN_PACKET_SET_CURRENT_BRAKE_REL,
	CAN_PACKET_SET_CURRENT_HANDBRAKE,
	CAN_PACKET_SET_CURRENT_HANDBRAKE_REL
}
CAN_PACKET_MODE_ID;
#endif
```

### 3 float value

​      /* --- erpm: 1 ~ 1 rpm --- */

​      /* --- value: [-erpm_max,erpm_max] 1rpm --- */



​      /* --- pos: 1e6f ~ 1 degree --- */

​      /* --- value: [-inf,+inf] 1degree --- */

余下其他模式的value可参考`HAL_StatusTypeDef can_send_command(VESC_t *hvesc, const CAN_PACKET_MODE_ID id, float value,int all)`函数的定义

### 4 int all










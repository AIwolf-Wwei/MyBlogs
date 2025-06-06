---
title: "CANopenNode|从零开始使用"
date: 2025-05-22
---

# 1. 从零开始移植CANopenNode协议栈

## 材料准备

1. [CANopenNode协议栈](https://github.com/CANopenNode/CANopenNode)

2. [CANopenEditor对象字典编辑器](https://github.com/CANopenNode/CANopenEditor?tab=readme-ov-file)

3. [CANopenSTM32](https://github.com/CANopenNode/CanOpenSTM32)

4. 最小系统板STM32G0B1RCT6TR

5. STM32cubeMX

6. STM32cubeIDE

# 2. 使用STM32cubeMX生成工程

![](https://i-blog.csdnimg.cn/direct/69dfc221143b4832b829881c766962da.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![](https://i-blog.csdnimg.cn/direct/cb544c3b468a41b7b8c085f034b8b888.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

![](https://i-blog.csdnimg.cn/direct/c8f5c26e0e5c47a7b92ea0569232e1ce.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![](https://i-blog.csdnimg.cn/direct/72f0de9d29914a5eb23673b8ce2fd3df.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![](https://i-blog.csdnimg.cn/direct/afe5137c2b50448bad81a16f46e222c1.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![](https://i-blog.csdnimg.cn/direct/6ed1f72bc13d4d0ab074e6b20448daaa.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![](https://i-blog.csdnimg.cn/direct/d624277396ff40d0b9cc7127117f6edd.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![](https://i-blog.csdnimg.cn/direct/7704968fc5c74b0e8b5c5d967ab2719a.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

![](https://i-blog.csdnimg.cn/direct/c34d333020964638be1c4544a10e94bd.png)

​

 生成工程，使用STM32CubeIDE打开

![](https://i-blog.csdnimg.cn/direct/6617e541207443dbb5d699b2d5cd4d7b.png)

​在main.c文件中添加代码

```c
/* USER CODE BEGIN 4 */
//printf
#ifdef __GNUC__
/* With GCC/RAISONANCE, small printf (option LD Linker->Libraries->Small printfset to 'Yes') calls __io_putchar() */
#define PUTCHAR_PROTOTYPE int __io_putchar(int ch)
#else
#define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)
#endif /* __GNUC__ */
/*** @brief Retargets the C library printf function to the USART.* @param None* @retval None*/
PUTCHAR_PROTOTYPE
{
    /* Place your implementation of fputc here */
    /* e.g. write a character to the USART1 and Loop until the end of transmission */
    HAL_UART_Transmit(&huart3, (uint8_t *)&ch, 1, 0xFFFF);

    return ch;
}
/* USER CODE END 4 */
```

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​![](https://i-blog.csdnimg.cn/direct/48705ce4c6394abfa04a3a0804e2b1d2.png)

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

 串口功能调试

![](https://i-blog.csdnimg.cn/direct/7f42b97451e74a42abb1fbd73e1aa441.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

# 3. 移植CANopenNode

如下图所示将3个文件夹复制到工程文件

![](https://i-blog.csdnimg.cn/direct/ecae6be1ff264a2f8b701d05df4ec715.png)

![](https://i-blog.csdnimg.cn/direct/808c633b6f3b4c389aeb62f72ef3f86d.png)

以上为CANopenNode文件夹中内容

![](https://i-blog.csdnimg.cn/direct/d54ddfb65f66421a81f66eb1fe184e5e.png)

以上为CANopenSTM32文件夹中内容

按照下图添加头文件路径

![](https://i-blog.csdnimg.cn/direct/320f396f8f2143be97e8334ed8fd0a3e.png)

根据下图添加源文件路径

![](https://i-blog.csdnimg.cn/direct/1d33db79226b441da5c9c9f4ba974c84.png)

    ​在main.c中添加修改代码

```c
/* USER CODE BEGIN Includes */
#include "CO_app_STM32.h"
/* USER CODE END Includes */
```

```c
/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */
// Timer interrupt function executes every 1 ms
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef* htim)
{
    if (htim == canopenNodeSTM32->timerHandle) {
        canopen_app_interrupt();
    }

}
/* USER CODE END 0 */
```

```c
  /* USER CODE BEGIN 2 */
  CANopenNodeSTM32 canOpenNodeSTM32;
  canOpenNodeSTM32.CANHandle = &hfdcan1;
  canOpenNodeSTM32.HWInitFunction = MX_FDCAN1_Init;
  canOpenNodeSTM32.timerHandle = &htim7;
  canOpenNodeSTM32.desiredNodeID = 3;
  canOpenNodeSTM32.baudrate = 500;
  canopen_app_init(&canOpenNodeSTM32);
  /* USER CODE END 2 */
```

```c
  /* USER CODE BEGIN WHILE */
  while (1)
  {
//    printf("Test uart communicaion\n");
    canopen_app_process();
    /* USER CODE END WHILE */
```

![](https://i-blog.csdnimg.cn/direct/e1e5954420ec46fa91099de588037a12.png)

​编辑对象字典

![](https://i-blog.csdnimg.cn/direct/ade754a7c2c446dcbc228aaddf4b0c97.png)

![](https://i-blog.csdnimg.cn/direct/52d23d0712bc48918233720d6b23aecc.png)

![](https://i-blog.csdnimg.cn/direct/275590c8684141cdae8719b0730bc544.png)

![](https://i-blog.csdnimg.cn/direct/8a6b3325b936405392f5e9bf3e978724.png)

# 4. NMT

![](https://i-blog.csdnimg.cn/direct/c74b01ee7aa5444495aa54256834d2d3.png)

![](https://i-blog.csdnimg.cn/direct/4bf2f6838b2d471692cc82917750d839.png)

![](https://i-blog.csdnimg.cn/direct/8f41a2197ad94afdae35edd21a6e7589.png)

|      | CAN-ID | CS命令符 | 数据：Node-ID |          |
| ---- | ------ | ----- | ---------- | -------- |
| 主机发送 | 0x000h | 0x02h | 03         | 命令进入停止状态 |
| 从机应答 | 0x703h | -     | 04         | 停止状态     |

![](https://i-blog.csdnimg.cn/direct/c8fb633982944654a7c25ac18de3f9d3.png)

|      | CAN-ID | CS命令符 | 数据：Node-ID |          |
| ---- | ------ | ----- | ---------- | -------- |
| 主机发送 | 0x000h | 0x01h | 03         | 命令进入操作状态 |
| 从机应答 | 0x703h | -     | 05         | 操作状态     |

![](https://i-blog.csdnimg.cn/direct/3bec3f307b1d41cab56e870d04f4e739.png)

|      | CAN-ID | CS命令符 | 数据：Node-ID |         |
| ---- | ------ | ----- | ---------- | ------- |
| 主机发送 | 0x000h | 0x81h | 03         | 命令复位应用层 |
| 从机应答 | 0x703h | -     | 00         | 复位后自动上线 |

![](https://i-blog.csdnimg.cn/direct/7480c9c85217460c9d5dfceea108cdc5.png)

|      | CAN-ID | CS命令符 | 数据：Node-ID |          |
| ---- | ------ | ----- | ---------- | -------- |
| 主机发送 | 0x000h | 0x81h | 03         | 命令复位节点通信 |
| 从机应答 | 0x703h | -     | 00         | 复位后自动上线  |

![](https://i-blog.csdnimg.cn/direct/143a773eed57487b840ef666b581f96d.png)

# 5. SDO

![](https://i-blog.csdnimg.cn/direct/84d4966a06fd44aa8a0d15822289aa29.png)

![](https://i-blog.csdnimg.cn/direct/d28536cb7ee7458090fb659546d3d658.png)

|       | CAN-ID | 数据：Node-ID（注意大小端问题）       |                                 |
| ----- | ------ | ------------------------- | ------------------------------- |
| 客户端发送 | 0x603h | 0x40 17 10 00 00 00 00 00 | 读取03节点的主索引1017子索引00 的数据内容       |
| 服务器应答 | 0x583h | 0x4B 17 10 00 E8 03 00 00 | 主索引1017子索引00返回两个字节数据内容为 0x03 E8 |

![](https://i-blog.csdnimg.cn/direct/10d1acf42f27426c9ddbab9c91b4f3ce.png)

|       | CAN-ID | 数据：Node-ID（注意大小端问题）       |                                   |
| ----- | ------ | ------------------------- | --------------------------------- |
| 客户端发送 | 0x603h | 0x2B 17 10 00 D0 07 00 00 | 写入03节点的主索引1017子索引00 的数据内容为0x07 D0 |
| 服务器应答 | 0x583h | 0x60 17 10 00 00 00 00 00 | 主索引1017子索引00写入两个字节数据内容成功          |

![](https://i-blog.csdnimg.cn/direct/3a6a6c1858544968b8e4d7f640137736.png)

### 在工程中添加如下函数进行SDO 读写操作

```c
/*
*********************************************************************************************************
*        read_SDO
*********************************************************************************************************
*/
CO_SDO_abortCode_t read_SDO(CO_SDOclient_t *SDO_C, uint8_t nodeId,
                            uint16_t index, uint8_t subIndex,
                            uint8_t *buf, size_t bufSize, size_t *readSize)
{
    CO_SDO_return_t SDO_ret;

    // setup client (this can be skipped, if remote device don't change)
    SDO_ret = CO_SDOclient_setup(SDO_C,
                                 CO_CAN_ID_SDO_CLI + nodeId,
                                 CO_CAN_ID_SDO_SRV + nodeId,
                                 nodeId);
    if (SDO_ret != CO_SDO_RT_ok_communicationEnd) {
        return CO_SDO_AB_GENERAL;
    }

    // initiate upload
    SDO_ret = CO_SDOclientUploadInitiate(SDO_C, index, subIndex, 1000, false);
    if (SDO_ret != CO_SDO_RT_ok_communicationEnd) {
        return CO_SDO_AB_GENERAL;
    }

    // upload data
    do {
        uint32_t timeDifference_us = 10000;
        CO_SDO_abortCode_t abortCode = CO_SDO_AB_NONE;

        SDO_ret = CO_SDOclientUpload(SDO_C,
                                     timeDifference_us,
                                     false,
                                     &abortCode,
                                     NULL, NULL, NULL);
        if (SDO_ret < 0) {
            return abortCode;
        }

        bsp_DelayUS(timeDifference_us);
    } while(SDO_ret > 0);

    // copy data to the user buffer (for long data function must be called
    // several times inside the loop)
    *readSize = CO_SDOclientUploadBufRead(SDO_C, buf, bufSize);

    return CO_SDO_AB_NONE;
}

/*
*********************************************************************************************************
*         write_SDO
*********************************************************************************************************
*/
CO_SDO_abortCode_t write_SDO(CO_SDOclient_t *SDO_C, uint8_t nodeId,
                             uint16_t index, uint8_t subIndex,
                             uint8_t *data, size_t dataSize)
{
    CO_SDO_return_t SDO_ret;
    bool_t bufferPartial = false;

    // setup client (this can be skipped, if remote device is the same)
    SDO_ret = CO_SDOclient_setup(SDO_C,
                                 CO_CAN_ID_SDO_CLI + nodeId,
                                 CO_CAN_ID_SDO_SRV + nodeId,
                                 nodeId);
    if (SDO_ret != CO_SDO_RT_ok_communicationEnd) {
        return -1;
    }

    // initiate download
    SDO_ret = CO_SDOclientDownloadInitiate(SDO_C, index, subIndex,
                                           dataSize, 1000, false);
    if (SDO_ret != CO_SDO_RT_ok_communicationEnd) {
        return -1;
    }

    // fill data
    size_t nWritten = CO_SDOclientDownloadBufWrite(SDO_C, data, dataSize);
    if (nWritten < dataSize) {
        bufferPartial = true;
        // If SDO Fifo buffer is too small, data can be refilled in the loop.
    }

    //download data
    do {
        uint32_t timeDifference_us = 10000;
        CO_SDO_abortCode_t abortCode = CO_SDO_AB_NONE;

        SDO_ret = CO_SDOclientDownload(SDO_C,
                                       timeDifference_us,
                                       false,
                                       bufferPartial,
                                       &abortCode,
                                       NULL, NULL);
        if (SDO_ret < 0) {
            return abortCode;
        }

        bsp_DelayUS(timeDifference_us);
    } while(SDO_ret > 0);

    return CO_SDO_AB_NONE;
}
```

- CAN 网络中，SDO 客户端到服务器的报文 COB-ID 为 `0x600 + nodeId`，服务器到客户端的报文 COB-ID 为 `0x580 + nodeId`。
- 在实际应用中，需要根据具体需求调整对象字典中的索引和子索引，以及要写入或读取的数据。同时，要确保 CAN 总线的波特率和节点 ID 等参数配置正确，以保证通信的正常进行。
- 注意使用读写SDO函数时需要打开CO_SDOclient.h和CO_fifo.h中的配置参数，不然编译会报错。

# 6. PDO

发送节点的COB-ID一定要和接收节点的COB-ID后11位要一致，不然不能正常接收PDO报文信息。

## TPDO配置参数

![](https://i-blog.csdnimg.cn/direct/dc5cdc253f214611a5996605ce27aef5.png)

![](https://i-blog.csdnimg.cn/direct/81c3c26b81ed4c29ba57ed6e2f82b9ea.png)

![](https://i-blog.csdnimg.cn/direct/66ca6aeb68e44dea9c175ccceef0e9a8.png)

OD中参数发生变化后，需要调用CO_TPDOsendRequest()函数发送PDO请求。

```c
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
      /*    CANopen_app    */
            /*    update data    */
            OD_RAM.x6024_output1Actual.voltage++;
            OD_RAM.x6024_output1Actual.current++;
            OD_RAM.x6024_output1Actual.current++;
            /*    Start TPDO    */
            CO_TPDOsendRequest(&CO->TPDO[0]);
          /*    APP function    */
            canopen_app_process();

            HAL_Delay(2000);
      //printf("test");
  }
  /* USER CODE END 3 */ USER CODE END 3 */
```

## RPDO配置参数

![](https://i-blog.csdnimg.cn/direct/e957e765de1f43b1942bbce3a2d779ab.png)

![](https://i-blog.csdnimg.cn/direct/5212ace7709d4be4a643f1868a9eb659.png)

接收端在通信正常的情况下，默认无需处理。OD中的数据会自动跟随RPDO的接收而更新，程序中可以通过轮询查看OD的数据进行必要的其他程序调用。

```c
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
    /* Printf RPDO data */  
    printf("RPDO data OD_RAM.x6024_output1Actual.voltage %d \n",OD_RAM.x6024_output1Actual.voltage);
    printf("RPDO data OD_RAM.x6024_output1Actual.voltage %d \n",OD_RAM.x6024_output1Actual.current);
    canopen_app_process();
    HAL_Delay(500);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */ODE END 3 */
```

## 同步报文

![](https://i-blog.csdnimg.cn/direct/b48fc7e75c304f3a98b29159fe50bab5.png)

每个节点都以主机的同步报文作为PDO触发参数，因此同步报文的COB-ID具有较高的优先级以及最短的传输时间，一般选用80h作为同步报文的COB-ID。

同步报文涉及三个索引，分别是0x1005，0x1006，0x1007。

![](https://i-blog.csdnimg.cn/direct/cf6e3be0adf04b2baeeebebb6f996212.png)

![](https://i-blog.csdnimg.cn/direct/94779db51def4e17bb1863fecb71bbc0.png)

![](https://i-blog.csdnimg.cn/direct/76feed29f9f54b7d89ebf4300f6b33dd.png)

key value 根据关键字取值

#stm32_key_value      stm32 f1 f4 L151系列键值对存储；支持4字节整型数据，字符串数据。仅仅支持stm32内部flash存储数据。

友情链接:支持外部flash存储的另一个开源项目https://github.com/armink/EasyFlash.git

可能产生哈希冲突，需要检测，检查接口  check_hash_conflict( 5, "liang", "zhang", "gan", "hao", "liu" );

配置:

CORTEX_M3表示F1和L151系列

CORTEX_M3表示F4系列

#define _STM32L_            //表示stm32L151系列，因为stm32L系列，stm8S系列，stm8L系列flash属性和F1、F4不一样，因此坐特殊处理

transplant.h文件配置相应宏

#define SYS  false                                   //true带freeRTOS   false不带freeRTOS

#define SECTOR_NUM        8                         //stm32f407vet6有8个扇区，因此配置成8，具体可以查询j-flash工具

#define KEY_VALUE_SIZE    ( 128 * 1024 )            //使用了5/6/7扇区，最小一个扇区是128KB，所以填128*1024;如果选择1/2/3扇区，最小一个扇区是
16KB，那么就填写16*1024

#define FLASH_MAX_SIZE    ( 512 * 1024 )            //stm32f407vet6芯片内部flash大小为512KB

#define FLASH_END_ADDR    ( FLASH_BASE + FLASH_MAX_SIZE )//最大的flash地址

uint32_t flash_sector_address( int16_t index )      //根据相应stm32芯片内部flash填写这个函数即可，仅仅这个函数需要重写；根据第几个扇区获取当前扇区
的有效地址。

测试过:stm32l151c8、stm32f407vet6、stm32f103rct6、stm32f103zet6、stm32f103c8t6,运行非常稳定


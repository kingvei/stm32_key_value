#stm32_key_value

使用stm32内部flash作为键值对的存储，掉电保存数据

可能产生哈希冲突，需要检测，检查接口check_hash_conflict( 5, "liang", "zhang", "gan", "hao", "liu" );

只能存储INT32整型数据和可见字符串数据

初始化:

#define  ADDRESS_MAPPING(X)         (0x8000000+X*2*1024)   //flash扇区

init_key_value( ADDRESS_MAPPING(116), ADDRESS_MAPPING(117), ADDRESS_MAPPING(118) );

基于freeRTOS系实时操作系统，使用互斥信号量来使用set和get value


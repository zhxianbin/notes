[TOC]
----

# ����һ�������Լ���AVR��RTOS


�����Դ�03���������Ե�Ƭ����RTOS��ѧϰ��Ӧ�õ��ȳ���νһ�˸߹�һ��.03�꣬���뿪У԰ǰ�ģ��ǵ���Ǽ����£��ڻ�ʦ�ĺ����������˱��۱����ġ�UCOSII����ͨ���˼��Σ�û��ʵ�����ģ�Ҳ������֮��
������21IC�ϣ���Ҷ����Կ�������д�Ĺ���UCOSII��51�ϵ���ֲ������������51�ϵ�RTOS���ȳ���
�����ٺ����������������Ƴ���small rots��չʾ��һ������51�ϵ�΢�ںˣ�������52�Ͻ���������ȡ�
����ǰ��ʱ�䣬��ouravr���濪��ר�Ź���AVR��Rtos��ר�������Ҳ��ٵ��ֵܰ��Լ�����Ʒ�ó�������ʵ���˲����۽硣��ʱ�������»ع���ʹ�õ�Ƭ���ľ��������ú��б�Ҫ���Ӹ����϶Ե�Ƭ����RTOS��֪ʶ�����������ǣ��ҿ�ʼ�˱�дһ������AVR��Ƭ����RTOS��
������ʱ�������е�֪ʶ����Դ�У�
����Proteus6.7 ��������ģ�����avrϵ�еĵ�Ƭ��
����WinAVR v2.0.5.48 ����GCC AVR�ı��뻷�����ô����ڿ�����C�����в���asm�����
����mega8 1K��ram��8K��rom,�ǿ���8λ��RTOS��һ������������������Ҷ���Ҳ�Ƚ���Ϥ��
����дUCOS��Jean J.Labrosse����������������һ�仰���������أ�����Ȼ���뵽��д��ʵʱ�ں�ֱ����ô����?�����ǲ��ϵر��棬�ָ�CPU����Щ�Ĵ������
�������ˣ�����һ��׼���ú����ǾͿ��Կ�ʼ���ǵ�Rtos for mega8��ʵ��֮���ˡ�
���������г������ӣ�ȫ���������á�ֻ��Ҫһ���ļ��Ϳ��Ա����ˡ������ţ�ֻҪ�ʵ����ã���򵥵ľ�����õģ����������ų�һЩ����Ҫ�ĸ��ţ��ô��רע��ÿһ�����̵�ѧϰ��
������һƪ������������
������һ��ĵ�Ƭ��ϵͳ�У�����ǰ��̨�ķ�ʽ(��ѭ�� �ж�)���������ݺ�������Ӧ�ġ�
������������:
����makefile���趨:����WinAvr�е�Mfile���趨����
����MCU Type: mega8
����Optimization level: s
����Debug format :AVR-COFF
����C/C source file: ѡ��Ҫ�����C�ļ�
#include  <avr/io.h>

void fun1(void) 
{ 
    unsigned char i=0; 

    while(1) 
    { 
        PORTB=i ; 
        PORTC=0x01<<(i%8); 
    } 
} 

int main(void) 
{ 
    fun1(); 
}
�������ȣ����һ�����⣺���Ҫ����һ������������ֻ��������ķ�ʽ������?
��������ѧϰ��C���Եĸ�λ��ش�No!���ǻ���һ�ַ�ʽ�����ǡ��ú���ָ��������ú������������Ҷ�����һ���������Ľ̿�����̷��ǿ�����ġ�C������ơ��Ļ������һ���ĵ�9.5�ڡ�
�������ӣ��ú���ָ��������ú���
����#include
����void fun1(void)
����{
����unsigned char i=0;
����while(1)
����{
����PORTB=i ;
����PORTC=0x01<<(i%8);
����}
����}
����void (*pfun)(); //ָ������ָ��
����int main(void)
����{
����pfun=fun1; //
����(*pfun)(); //����ָ����ָ��ĺ���
����}
�����ڶ��֣��ǡ���ָ������ָ�����������������
����#include
����void fun1(void)
����{
����unsigned char i=0;
����while(1)
����{
����PORTB=i ;
����PORTC=0x01<<(i%8);
����}
����}
����void RunFun(void (*pfun)()) //�����Ҫ���ݵĺ����ĵ�ַ
����{
����(*pfun)(); //��RunFun�У�����ָ����ָ��ĺ���
����}
����int main(void)
����{
����RunFun(fun1); //��������ָ����Ϊ��������
����}
����������������ַ�ʽ���ܶ��˿��ܻ�˵�������ȷ����������������������Ҫ��RTOS����ʲô��ϵ��?��λ��ϸ�����¿���
����������GCC������Ĵ���ı���������
������main()�е�RunFun(fun1); �ı�������
����ldi r24,lo8(pm(fun1))
����ldi r25,hi8(pm(fun1))
����rcall RunFun
������void RunFun(void (*pfun)())�ı�������
����/*void RunFun(void (*pfun)())*/
����/*(*pfun)();*/
����.LM6:
����movw r30,r24
����icall
����ret
�����ڵ���void RunFun(void (*pfun)())��ʱ�򣬵�ȷ���԰�fun1�ĵ�ַͨ��r24��r25���ݸ�RunFun()�����ǣ�RTOS��β�����Ч�����ú����ĵ�ַ��?
�����ڶ�ƪ�� �˹���ջ
�����ڵ�Ƭ����ָ��У�һ��ָ����ר�����ջ��PCָ�����ģ�������
����rcall ��Ե����ӳ���ָ��
����icall ��ӵ����ӳ���ָ��
����ret �ӳ��򷵻�ָ��
����reti �жϷ���ָ��
��������ret��reti�����Ƕ����Խ���ջջ���������ֽڱ�������������������PC�У�һ���������ӳ�����ж����˳�������reti���������˳��ж�ʱ���ؿ�ȫ���ж�ʹ�ܡ�
������������������Ϳ��Խ������ǵ��˹���ջ�ˡ�
��������
����#include
����void fun1(void)
����{
����unsigned char i=0;
����while(1)
����{
����PORTB=i ;
����PORTC=0x01<<(i%8);
����}
����}
����unsigned char Stack[100]; //����һ��100�ֽڵ��˹���ջ
����void RunFunInNewStack(void (*pfun)(),unsigned char *pStack)
����{
����*pStack--=(unsigned int)pfun>>8; //�������ĵ�ַ��λѹ���ջ��
����*pStack--=(unsigned int)pfun; //�������ĵ�ַ��λѹ���ջ��
����SP=pStack; //����ջָ��ָ���˹���ջ��ջ��
����__asm__ __volatile__("RET \n\t"); //���ز����ж�,��ʼ����fun1()
����}
����int main(void)
����{
����RunFunInNewStack(fun1,&Stack[99]);
����}
����RunFunInNewStack(),��ָ������ָ���ֵ���浽һ��unsigned char������Stack�У���Ϊ�˹���ջ�����ҽ�ջ������ֵ�������ջָ��SP,��˵���"ret"����ʱ����SP�лָ���PC�е�ֵ���ͱ�Ϊ��ָ��fun1()�ĵ�ַ����ʼ����fun1().
����������������RunFunInNewStack()�����һ��Ƕ���˻����� "ret",ʵ�����ǿ���ȥ���ġ���Ϊ��RunFunInNewStack()����ʱ���������Ѿ������"ret"��������д��������Ϊ���ô�ҿ�����"ret"��Ϊ���غ�����fun1()�Ĺ��̡�
��������ƪ��GCC�жԼĴ����ķ�����ʹ��
�����ںܶ�����AVR��RTOS�У��������������ʱ���������µ���䣺
������ջ��
����__asm__ __volatile__("PUSH R0 \n\t");
����__asm__ __volatile__("PUSH R1 \n\t");
����......
����__asm__ __volatile__("PUSH R31 \n\t");
������ջ
����__asm__ __volatile__("POP R31 \n\t");
����......
����__asm__ __volatile__("POP R1 \n\t");
����__asm__ __volatile__("POP R0 \n\t");
����ͨ����Ҷ�����Ϊ����������ȿ�ʼʱ����ȻҪ�����е�ͨ�üĴ��������棬���һ�Ӧ�ñ������״̬�Ĵ���SREG��Ȼ���ٸ����෴�Ĵ��򣬽�������ļĴ��������ݻָ���
�������ǣ���ʵ�����������?�����ҿ�������������д��small rots51,�ͻᷢ�֣����������ͨ�üĴ���������4��ͨ�üĴ����е�1�顣
������Win AVR�еİ����ļ� avr-libc Manual�е�Related Pages�е�Frequently Asked Questions,��ʵ��һ��������"What registers are used by the C compiler?" �ش��˱���������Ҫռ�õļĴ�����һ������£������������õ����¼Ĵ���
����1 Call-used registers (r18-r27, r30-r31): ���ú���ʱ��Ϊ�������ݣ�Ҳ�����õ����ļĴ�����
����2 Call-saved registers (r2-r17, r28-r29): ���ú���ʱ��Ϊ�������,���е�r28��r29���ܻᱻ��Ϊָ���ջ�ϵı�����ָ�롣
����3 Fixed registers (r0, r1): �̶����á�r0���ڴ����ʱ���ݣ�r1���ڴ��0��
����������һ��������"How to permanently bind a variable to a register?",�ǽ������󶨵�ͨ�üĴ����ķ����������ҷ��֣������ĳ���Ĵ�������Ϊ�������������ͻ᲻���üĴ���������������;�����RTOS�Ǻ���Ҫ�ġ�
������"Inline Asm"�е�"C Names Used in Assembler Code"��ȷ��ʾ,�����̫���ͨ�üĴ�������Ϊ���������ڱ���Ĺ����У�������ı�����Ȼ���ܱ�������ռ�á�
������ҿ��ԱȽ������������ӣ����������������Ĵ��룺(��*.lst�ļ���)
������һ�����ӣ�û�ж���ͨ�üĴ���Ϊ����
����#include
����unsigned char add(unsigned char b,unsigned char c,unsigned char d)
����{
����return b c*d;
����}
����int main(void)
����{
����unsigned char a=0;
����while(1)
����{
����a ;
����PORTB=add(a,a,a);
����}
����}
�����ڱ����У�"add(a,a,a);"����������:
����mov r20,r28
����mov r22,r28
����mov r24,r28
����rcall add
�����ڶ������ӣ�����ͨ�üĴ���Ϊ����
����#include
����unsigned char add(unsigned char b,unsigned char c,unsigned char d)
����{
����return b c*d;
����}
����register unsigned char a asm("r20"); //��r20����Ϊ ����a
����int main(void)
����{
����while(1)
����{
����a ;
����PORTB=add(a,a,a);
����}
����}
�����ڱ����У�"add(a,a,a);"����������:
����mov r22,r20
����mov r24,r20
����rcall add
������Ȼ�����������������У��в��ݴ��뱻�������Ż��ˡ�
����ͨ���������ԣ����ֱ�����һ��ʹ�����¼Ĵ���:
������1��Ĵ�������2��Ĵ�����r28,r29,��3��Ĵ���
���������жϺ������е��û����������ջ��ڽ����жϺ󣬹̶��ؽ���1��Ĵ����͵�3��Ĵ�����ջ�����˳��ж��ֽ����ǳ�ջ��
��������ƪ��ֻ����ʱ�����Э��ʽ���ں�
����Cooperative Multitasking
����ǰ��̨ϵͳ��Э��ʽ�ں�ϵͳ����ռ��ʽ�ں�ϵͳ����ʲô��ͬ��?
�����ǵ���21IC�Ͽ��������ı���,����(С��)���ò����������������ŵ�һ���ϰ��������ŵڶ��������ǰ��̨��������˭�������밴�ŶӵĴ���ʹ�ò���;�����Э��ʽ����ô���Ե�������������ϰ��Ҫ�Ⱦ����Ƚ���;�����ռ��ʽ��ֻҪ�и��߼�����������ȣ���ô������������˭����Ҫ��һʱ���ó���������߼���������á���
����#include
����#include
����#include
����unsigned char Stack[200];
����register unsigned char OSRdyTbl asm("r2"); //�������о�����
����register unsigned char OSTaskRunningPrio asm("r3"); //�������е�����
����#define OS_TASKS 3 //�趨�������������
����struct TaskCtrBlock //������ƿ�
����{
����unsigned int OSTaskStackTop; //��������Ķ�ջ��
����unsigned int OSWaitTick; //������ʱʱ��
����} TCB[OS_TASKS 1];
����//��ֹ��������ռ��
����register unsigned char tempR4 asm("r4");
����register unsigned char tempR5 asm("r5");
����register unsigned char tempR6 asm("r6");
����register unsigned char tempR7 asm("r7");
����register unsigned char tempR8 asm("r8");
����register unsigned char tempR9 asm("r9");
����register unsigned char tempR10 asm("r10");
����register unsigned char tempR11 asm("r11");
����register unsigned char tempR12 asm("r12");
����register unsigned char tempR13 asm("r13");
����register unsigned char tempR14 asm("r14");
����register unsigned char tempR15 asm("r15");
����register unsigned char tempR16 asm("r16");
����register unsigned char tempR16 asm("r17");
����//��������
����void OSTaskCreate(void (*Task)(void),unsigned char *Stack,unsigned char TaskID)
����{
����unsigned char i;
����*Stack--=(unsigned int)Task>>8; //������ĵ�ַ��λѹ���ջ��
����*Stack--=(unsigned int)Task; //������ĵ�ַ��λѹ���ջ��
����*Stack--=0x00; //R1 __zero_reg__
����*Stack--=0x00; //R0 __tmp_reg__
����*Stack--=0x80; //SREG �������У�����ȫ���ж�
����for(i=0;i<14;i ) //�� avr-libc �е� FAQ�е� What registers are used by the C compiler?
����*Stack--=i; //�����˼Ĵ���������
����TCB[TaskID].OSTaskStackTop=(unsigned int)Stack; //���˹���ջ��ջ�������浽��ջ��������
����OSRdyTbl|=0x01<
����}
����//��ʼ�������,��������ȼ�������Ŀ�ʼ
����void OSStartTask()
����{
����OSTaskRunningPrio=OS_TASKS;
����SP=TCB[OS_TASKS].OSTaskStackTop 17;
����__asm__ __volatile__( "reti" "\n\t" );
����}
����//�����������
����void OSSched(void)
����{
����// �����ж�ʱ����Ĵ����Ĵ�����ջ��ģ��һ���жϺ���ջ�����
����__asm__ __volatile__("PUSH __zero_reg__ \n\t"); //R1
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t"); //R0
����__asm__ __volatile__("IN __tmp_reg__,__SREG__ \n\t"); //����״̬�Ĵ���SREG
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t");
����__asm__ __volatile__("CLR __zero_reg__ \n\t"); //R0��������
����__asm__ __volatile__("PUSH R18 \n\t");
����__asm__ __volatile__("PUSH R19 \n\t");
����__asm__ __volatile__("PUSH R20 \n\t");
����__asm__ __volatile__("PUSH R21 \n\t");
����__asm__ __volatile__("PUSH R22 \n\t");
����__asm__ __volatile__("PUSH R23 \n\t");
����__asm__ __volatile__("PUSH R24 \n\t");
����__asm__ __volatile__("PUSH R25 \n\t");
����__asm__ __volatile__("PUSH R26 \n\t");
����__asm__ __volatile__("PUSH R27 \n\t");
����__asm__ __volatile__("PUSH R30 \n\t");
����__asm__ __volatile__("PUSH R31 \n\t");
����__asm__ __volatile__("PUSH R28 \n\t"); //R28��R29���ڽ����ڶ�ջ�ϵ�ָ��
����__asm__ __volatile__("PUSH R29 \n\t"); //��ջ���
����TCB[OSTaskRunningPrio].OSTaskStackTop=SP; //���������е�����Ķ�ջ�ױ���
����unsigned char OSNextTaskID; //�����ж�ջ�Ͽ����µĿռ�
����for (OSNextTaskID = 0; //�����������
����OSNextTaskID < OS_TASKS && !(OSRdyTbl & (0x01<
����OSNextTaskID );
����OSTaskRunningPrio = OSNextTaskID ;
����cli(); //������ջת��
����SP=TCB[OSTaskRunningPrio].OSTaskStackTop;
����sei();
����//�����ж�ʱ�ĳ�ջ����
����__asm__ __volatile__("POP R29 \n\t");
����__asm__ __volatile__("POP R28 \n\t");
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("POP R30 \n\t");
����__asm__ __volatile__("POP R27 \n\t");
����__asm__ __volatile__("POP R26 \n\t");
����__asm__ __volatile__("POP R25 \n\t");
����__asm__ __volatile__("POP R24 \n\t");
����__asm__ __volatile__("POP R23 \n\t");
����__asm__ __volatile__("POP R22 \n\t");
����__asm__ __volatile__("POP R21 \n\t");
����__asm__ __volatile__("POP R20 \n\t");
����__asm__ __volatile__("POP R19 \n\t");
����__asm__ __volatile__("POP R18 \n\t");
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //SERG ��ջ���ָ�
����__asm__ __volatile__("OUT __SREG__,__tmp_reg__ \n\t"); //
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //R0 ��ջ
����__asm__ __volatile__("POP __zero_reg__ \n\t"); //R1 ��ջ
����//�ж�ʱ��ջ���
����}
����void OSTimeDly(unsigned int ticks)
����{
����if(ticks) //����ʱ��Ч
����{
����OSRdyTbl &= ~(0x01<
����TCB[OSTaskRunningPrio].OSWaitTick=ticks;
����OSSched(); //���µ���
����}
����}
����void TCN0Init(void) // ��ʱ��0
����{
����TCCR0 = 0;
����TCCR0 |= (1<
����TIMSK |= (1<
����TCNT0 = 100; // �ü�����ʼֵ
����}
����SIGNAL(SIG_OVERFLOW0)
����{
����unsigned char i;
����for(i=0;i
����{
����if(TCB[i].OSWaitTick)
����{
����TCB[i].OSWaitTick--;
����if(TCB[i].OSWaitTick==0) //������ʱ�ӵ�ʱ,�������ɶ�ʱ����ʱ�Ĳ���
����{
����OSRdyTbl |= (0x01<
����}
����}
����}
����TCNT0=100;
����}
����void Task0()
����{
����unsigned int j=0;
����while(1)
����{
����PORTB=j ;
����OSTimeDly(2);
����}
����}
����void Task1()
����{
����unsigned int j=0;
����while(1)
����{
����PORTC=j ;
����OSTimeDly(4);
����}
����}
����void Task2()
����{
����unsigned int j=0;
����while(1)
����{
����PORTD=j ;
����OSTimeDly(8);
����}
����}
����void TaskScheduler()
����{
����while(1)
����{
����OSSched(); //�������е���
����}
����}
����int main(void)
����{
����TCN0Init();
����OSRdyTbl=0;
����OSTaskRunningPrio=0;
����OSTaskCreate(Task0,&Stack[49],0);
����OSTaskCreate(Task1,&Stack[99],1);
����OSTaskCreate(Task2,&Stack[149],2);
����OSTaskCreate(TaskScheduler,&Stack[199],OS_TASKS);
����OSStartTask();
����}
����������������У�һ�б�úܼ򵥣������������е������񣬶�ͨ����ʱ��������������CPU�Ŀ���Ȩ��
������ʱ���ж��У��Ը�������ĵ���ʱ���м�ʱ�����ĳ���������ʱ�����������������ھ���������λ��
������ͼ���ϵͳ����TaskScheduler()���������������ڷ�����CPU�Ŀ���Ȩ��ʼ���ϵؽ��е��ȡ����ĳ�������ھ���������λ��ͨ�����ȣ�������߼���������м������С�
��������ƪ�� ���Ƶ�Э��ʽ���ں�
��������Ϊ�����Э��ʽ�ں����һЩOS��������ķ���
����1 �����������������
����2 �ź���(�ڱ�Ҫʱ�򣬿�����չ���������Ϣ����)
����3 ��ʱ
����#include
����#include
����#include
����unsigned char Stack[400];
����register unsigned char OSRdyTbl asm("r2"); //�������о�����
����register unsigned char OSTaskRunningPrio asm("r3"); //�������е�����
����#define OS_TASKS 3 //�趨�������������
����struct TaskCtrBlock
����{
����unsigned int OSTaskStackTop; //��������Ķ�ջ��
����unsigned int OSWaitTick; //������ʱʱ��
����} TCB[OS_TASKS 1];
����//��ֹ��������ռ��
����register unsigned char tempR4 asm("r4");
����register unsigned char tempR5 asm("r5");
����register unsigned char tempR6 asm("r6");
����register unsigned char tempR7 asm("r7");
����register unsigned char tempR8 asm("r8");
����register unsigned char tempR9 asm("r9");
����register unsigned char tempR10 asm("r10");
����register unsigned char tempR11 asm("r11");
����register unsigned char tempR12 asm("r12");
����register unsigned char tempR13 asm("r13");
����register unsigned char tempR14 asm("r14");
����register unsigned char tempR15 asm("r15");
����register unsigned char tempR16 asm("r16");
����register unsigned char tempR16 asm("r17");
����//��������
����void OSTaskCreate(void (*Task)(void),unsigned char *Stack,unsigned char TaskID)
����{
����unsigned char i;
����*Stack--=(unsigned int)Task>>8; //������ĵ�ַ��λѹ���ջ��
����*Stack--=(unsigned int)Task; //������ĵ�ַ��λѹ���ջ��
����*Stack--=0x00; //R1 __zero_reg__
����*Stack--=0x00; //R0 __tmp_reg__
����*Stack--=0x80;
����//SREG �������У�����ȫ���ж�
����for(i=0;i<14;i ) //�� avr-libc �е� FAQ�е� What registers are used by the C compiler?
����*Stack--=i; //�����˼Ĵ���������
����TCB[TaskID].OSTaskStackTop=(unsigned int)Stack; //���˹���ջ��ջ�������浽��ջ��������
����OSRdyTbl|=0x01<
����}
����//��ʼ�������,��������ȼ�������Ŀ�ʼ
����void OSStartTask()
����{
����OSTaskRunningPrio=OS_TASKS;
����SP=TCB[OS_TASKS].OSTaskStackTop 17;
����__asm__ __volatile__( "reti" "\n\t" );
����}
����//�����������
����void OSSched(void)
����{
����// �����ж�ʱ����Ĵ����Ĵ�����ջ��ģ��һ���жϺ���ջ�����
����__asm__ __volatile__("PUSH __zero_reg__ \n\t"); //R1
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t"); //R0
����__asm__ __volatile__("IN __tmp_reg__,__SREG__ \n\t"); //����״̬�Ĵ���SREG
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t");
����__asm__ __volatile__("CLR __zero_reg__ \n\t"); //R0��������
����__asm__ __volatile__("PUSH R18 \n\t");
����__asm__ __volatile__("PUSH R19 \n\t");
����__asm__ __volatile__("PUSH R20 \n\t");
����__asm__ __volatile__("PUSH R21 \n\t");
����__asm__ __volatile__("PUSH R22 \n\t");
����__asm__ __volatile__("PUSH R23 \n\t");
����__asm__ __volatile__("PUSH R24 \n\t");
����__asm__ __volatile__("PUSH R25 \n\t");
����__asm__ __volatile__("PUSH R26 \n\t");
����__asm__ __volatile__("PUSH R27 \n\t");
����__asm__ __volatile__("PUSH R30 \n\t");
����__asm__ __volatile__("PUSH R31 \n\t");
����__asm__ __volatile__("PUSH R28 \n\t"); //R28��R29���ڽ����ڶ�ջ�ϵ�ָ��
����__asm__ __volatile__("PUSH R29 \n\t"); //��ջ���
����TCB[OSTaskRunningPrio].OSTaskStackTop=SP; //���������е�����Ķ�ջ�ױ���
����unsigned char OSNextTaskID; //�����ж�ջ�Ͽ����µĿռ�
����for (OSNextTaskID = 0; //�����������
����OSNextTaskID < OS_TASKS && !(OSRdyTbl & (0x01<
����OSNextTaskID );
����OSTaskRunningPrio = OSNextTaskID ;
����cli(); //������ջת��
����SP=TCB[OSTaskRunningPrio].OSTaskStackTop;
����sei();
����//�����ж�ʱ�ĳ�ջ����
����__asm__ __volatile__("POP R29 \n\t");
����__asm__ __volatile__("POP R28 \n\t");
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("POP R30 \n\t");
����__asm__ __volatile__("POP R27 \n\t");
����__asm__ __volatile__("POP R26 \n\t");
����__asm__ __volatile__("POP R25 \n\t");
����__asm__ __volatile__("POP R24 \n\t");
����__asm__ __volatile__("POP R23 \n\t");
����__asm__ __volatile__("POP R22 \n\t");
����__asm__ __volatile__("POP R21 \n\t");
����__asm__ __volatile__("POP R20 \n\t");
����__asm__ __volatile__("POP R19 \n\t");
����__asm__ __volatile__("POP R18 \n\t");
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //SERG ��ջ���ָ�
����__asm__ __volatile__("OUT __SREG__,__tmp_reg__ \n\t"); //
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //R0 ��ջ
����__asm__ __volatile__("POP __zero_reg__ \n\t"); //R1 ��ջ
����//�ж�ʱ��ջ���
����}
����////////////////////////////////////////////������
����//��������
����void OSTaskSuspend(unsigned char prio)
����{
����TCB[prio].OSWaitTick=0;
����OSRdyTbl &= ~(0x01<
����if(OSTaskRunningPrio==prio) //��Ҫ���������Ϊ��ǰ����
����OSSched(); //���µ���
����}
����//�ָ����� �����ñ�OSTaskSuspend�� OSTimeDly��ͣ������ָ�
����void OSTaskResume(unsigned char prio)
����{
����OSRdyTbl |= 0x01<
����TCB[prio].OSWaitTick=0; //��ʱ���ʱ��Ϊ0,��ʱ
����if(OSTaskRunningPrio>prio) //��Ҫ��ǰ��������ȼ���������λ����������ȼ�
����OSSched(); //���µ��� //���µ���
����}
����// ������ʱ
����void OSTimeDly(unsigned int ticks)
����{
����if(ticks) //����ʱ��Ч
����{
����OSRdyTbl &= ~(0x01<
����TCB[OSTaskRunningPrio].OSWaitTick=ticks;
����OSSched(); //���µ���
����}
����}
����//�ź���
����struct SemBlk
����{
����unsigned char OSEventType; //�ͺ� 0,�ź�����ռ��;1�ź���������
����unsigned char OSEventState; //״̬ 0,������;1,����
����unsigned char OSTaskPendTbl; //�ȴ��ź����������б�
����} Sem[10];
����//��ʼ���ź���
����void OSSemCreat(unsigned char Index,unsigned char Type)
����{
����Sem[Index].OSEventType=Type; //�ͺ� 0,�ź�����ռ��;1�ź���������
����Sem[Index].OSTaskPendTbl=0;
����Sem[Index].OSEventState=0;
����}
����//����ȴ��ź���,����
����unsigned char OSTaskSemPend(unsigned char Index,unsigned int Timeout)
����{
����//unsigned char i=0;
����if(Sem[Index].OSEventState) //�ź�����Ч
����{
����if(Sem[Index].OSEventType==0) //���Ϊ��ռ��
����Sem[Index].OSEventState = 0x00; //�ź�������ռ��������
����}
����else
����{ //�����źŵ�����ȴ���
����Sem[Index].OSTaskPendTbl |= 0x01<
����OSRdyTbl &= ~(0x01<
����TCB[OSTaskRunningPrio].OSWaitTick=Timeout; //����ʱΪ0�������޵ȴ�
����OSSched(); //���µ���
����if(TCB[OSTaskRunningPrio].OSWaitTick==0) return 0;
����}
����return 1;
����}
����//����һ���ź��������Դ�������жϷ���
����void OSSemPost(unsigned char Index)
����{
����if(Sem[Index].OSEventType) //��Ҫ����ź����ǹ�����
����{
����Sem[Index].OSEventState=0x01; //ʹ�ź�����Ч
����OSRdyTbl |=Sem [Index].OSTaskPendTbl; //ʹ�ڵȴ����źŵ������������
����Sem[Index].OSTaskPendTbl=0; //������еȴ����źŵĵȴ�����
����}
����else //��Ҫ����ź���Ϊ��ռ��
����{
����unsigned char i;
����for (i = 0; i < OS_TASKS && !(Sem[Index].OSTaskPendTbl & (0x01<
����if(i < OS_TASKS) //�����������Ҫ
����{
����Sem[Index].OSTaskPendTbl &= ~(0x01<
����OSRdyTbl |= 0x01<
����}
����else
����{
����Sem[Index].OSEventState =1; //ʹ�ź�����Ч
����}
����}
����}
����//��������һ���ź����������е���
����void OSTaskSemPost(unsigned char Index)
����{
����OSSemPost(Index);
����OSSched();
����}
����//���һ���ź���,ֻ�Թ����͵����á�
����//���ڶ�ռ�͵��ź�����������ռ�ú󣬾ͽ��ò��������ˡ�
����void OSSemClean(unsigned char Index)
����{
����Sem[Index].OSEventState =0; //Ҫ����ź�����Ч
����}
����void TCN0Init(void) // ��ʱ��0
����{
����TCCR0 = 0;
����TCCR0 |= (1<
����TIMSK |= (1<
����TCNT0 = 100; // �ü�����ʼֵ
����}
����SIGNAL(SIG_OVERFLOW0)
����{
����unsigned char i;
����for(i=0;i
����{
����if(TCB[i].OSWaitTick)
����{
����TCB[i].OSWaitTick--;
����if(TCB[i].OSWaitTick==0) //������ʱ�ӵ�ʱ,�������ɶ�ʱ����ʱ�Ĳ���
����{
����OSRdyTbl |= (0x01<
����}
����}
����}
����TCNT0=100;
����}
����void Task0()
����{
����unsigned int j=0;
����while(1)
����{
����PORTB=j ;
����OSTaskSuspend(1); //��������1
����OSTaskSemPost(0);
����OSTimeDly(50);
����OSTaskResume(1); //�ָ�����1
����OSSemClean(0);
����OSTimeDly(50);
����}
����}
����void Task1()
����{
����unsigned int j=0;
����while(1)
����{
����PORTC=j ;
����OSTimeDly(5);
����}
����}
����void Task2()
����{
����unsigned int j=0;
����while(1)
����{
����OSTaskSemPend(0,10);
����PORTD=j ;
����OSTimeDly(5);
����}
����}
����void TaskScheduler()
����{
����while(1)
����{
����OSSched(); //�������е���
����}
����}
����int main(void)
����{
����TCN0Init();
����OSRdyTbl=0;
����OSSemCreat(0,1); //���ź�����Ϊ������
����OSTaskCreate(Task0,&Stack[99],0);
����OSTaskCreate(Task1,&Stack[199],1);
����OSTaskCreate(Task2,&Stack[299],2);
����OSTaskCreate(TaskScheduler,&Stack[399],OS_TASKS);
����OSStartTask();
����}
��������ƪ:ʱ��Ƭ�ַ����ȷ����ں�
����Round-Robin Sheduling
����ʱ��Ƭ�ֵ����Ƿǳ���Ȥ�ġ���ƪ�е����ӣ�������3����������û�����ȼ�����ʱ���жϵĵ����£�ÿ����������������ͬ��ʱ�䡣������ں���û�м����������񣬸о��Ͼͺ�������������ѭ����ͬʱ���С�
��������ֻ���ṩ��һ����ʱ���жϽ��е��ȵ��ںˣ���ҿ��Ը����Լ�����Ҫ�������Ӧ�ķ���
����Ҫע�⵽:
����1,������ʱ���ж��ڵ����������л���������Ϊ�ڽ����ж�ʱ���Ѿ���һϵ�еļĴ�����ջ��
����2,���ж��ڽ��е��ȣ���ֱ��ͨ��"RJMP Int_OSSched"���������л��͵��ȵģ�����GCC AVR��һ���ص㣬Ϊ��C��д�ں��ṩ�˼���ķ��㡣
����3,���Ķ������ͬʱ��������Ķ������������� *.lst�ļ����������������кܴ�İ�����
����#include
����#include
����#include
����unsigned char Stack[400];
����register unsigned char OSRdyTbl asm("r2"); //�������о�����
����register unsigned char OSTaskRunningPrio asm("r3"); //�������е�����
����#define OS_TASKS 3 //�趨�������������
����struct TaskCtrBlock
����{
����unsigned int OSTaskStackTop; //��������Ķ�ջ��
����unsigned int OSWaitTick; //������ʱʱ��
����} TCB[OS_TASKS 1];
����//��ֹ��������ռ��
����register unsigned char tempR4 asm("r4");
����register unsigned char tempR5 asm("r5");
����register unsigned char tempR6 asm("r6");
����register unsigned char tempR7 asm("r7");
����register unsigned char tempR8 asm("r8");
����register unsigned char tempR9 asm("r9");
����register unsigned char tempR10 asm("r10");
����register unsigned char tempR11 asm("r11");
����register unsigned char tempR12 asm("r12");
����register unsigned char tempR13 asm("r13");
����register unsigned char tempR14 asm("r14");
����register unsigned char tempR15 asm("r15");
����register unsigned char tempR16 asm("r16");
����register unsigned char tempR16 asm("r17");
����//��������
����void OSTaskCreate(void (*Task)(void),unsigned char *Stack,unsigned char TaskID)
����{
����unsigned char i;
����*Stack--=(unsigned int)Task>>8; //������ĵ�ַ��λѹ���ջ��
����*Stack--=(unsigned int)Task; //������ĵ�ַ��λѹ���ջ��
����*Stack--=0x00; //R1 __zero_reg__
����*Stack--=0x00; //R0 __tmp_reg__
����*Stack--=0x80;
����//SREG �������У�����ȫ���ж�
����for(i=0;i<14;i ) //�� avr-libc �е� FAQ�е� What registers are used by the C compiler?
����*Stack--=i; //�����˼Ĵ���������
����TCB[TaskID].OSTaskStackTop=(unsigned int)Stack; //���˹���ջ��ջ�������浽��ջ��������
����OSRdyTbl|=0x01<
����}
����//��ʼ�������,��������ȼ�������Ŀ�ʼ
����void OSStartTask()
����{
����OSTaskRunningPrio=OS_TASKS;
����SP=TCB[OS_TASKS].OSTaskStackTop 17;
����__asm__ __volatile__( "reti" "\n\t" );
����}
����//�����������
����void OSSched(void)
����{
����// �����ж�ʱ����Ĵ����Ĵ�����ջ��ģ��һ���жϺ���ջ�����
����__asm__ __volatile__("PUSH __zero_reg__ \n\t"); //R1
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t"); //R0
����__asm__ __volatile__("IN __tmp_reg__,__SREG__ \n\t"); //����״̬�Ĵ���SREG
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t");
����__asm__ __volatile__("CLR __zero_reg__ \n\t"); //R0��������
����__asm__ __volatile__("PUSH R18 \n\t");
����__asm__ __volatile__("PUSH R19 \n\t");
����__asm__ __volatile__("PUSH R20 \n\t");
����__asm__ __volatile__("PUSH R21 \n\t");
����__asm__ __volatile__("PUSH R22 \n\t");
����__asm__ __volatile__("PUSH R23 \n\t");
����__asm__ __volatile__("PUSH R24 \n\t");
����__asm__ __volatile__("PUSH R25 \n\t");
����__asm__ __volatile__("PUSH R26 \n\t");
����__asm__ __volatile__("PUSH R27 \n\t");
����__asm__ __volatile__("PUSH R30 \n\t");
����__asm__ __volatile__("PUSH R31 \n\t");
����__asm__ __volatile__("Int_OSSched: \n\t"); //���ж�Ҫ����ȣ�ֱ�ӽ�������
����__asm__ __volatile__("PUSH R28 \n\t"); //R28��R29���ڽ����ڶ�ջ�ϵ�ָ��
����__asm__ __volatile__("PUSH R29 \n\t"); //��ջ���
����TCB[OSTaskRunningPrio].OSTaskStackTop=SP; //���������е�����Ķ�ջ�ױ���
����if( OSTaskRunningPrio>=OS_TASKS) //�������и�������û�����ȼ�
����OSTaskRunningPrio=0;
����//cli(); //������ջת��
����SP=TCB[OSTaskRunningPrio].OSTaskStackTop;
����//sei();
����//�����ж�ʱ�ĳ�ջ����
����__asm__ __volatile__("POP R29 \n\t");
����__asm__ __volatile__("POP R28 \n\t");
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("POP R30 \n\t");
����__asm__ __volatile__("POP R27 \n\t");
����__asm__ __volatile__("POP R26 \n\t");
����__asm__ __volatile__("POP R25 \n\t");
����__asm__ __volatile__("POP R24 \n\t");
����__asm__ __volatile__("POP R23 \n\t");
����__asm__ __volatile__("POP R22 \n\t");
����__asm__ __volatile__("POP R21 \n\t");
����__asm__ __volatile__("POP R20 \n\t");
����__asm__ __volatile__("POP R19 \n\t");
����__asm__ __volatile__("POP R18 \n\t");
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //SERG ��ջ���ָ�
����__asm__ __volatile__("OUT __SREG__,__tmp_reg__ \n\t"); //
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //R0 ��ջ
����__asm__ __volatile__("POP __zero_reg__ \n\t"); //R1 ��ջ
����__asm__ __volatile__("RETI \n\t"); //���ز����ж�
����//�ж�ʱ��ջ���
����}
����void IntSwitch(void)
����{
����__asm__ __volatile__("POP R31 \n\t"); //ȥ��������ӳ������ջ��PC
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("RJMP Int_OSSched \n\t"); //���µ���
����}
����void TCN0Init(void) // ��ʱ��0
����{
����TCCR0 = 0;
����TCCR0 |= (1<
����TIMSK |= (1<
����TCNT0 = 100; // �ü�����ʼֵ
����}
����SIGNAL(SIG_OVERFLOW0)
����{
����TCNT0=100;
����IntSwitch(); //�������
����}
����void Task0()
����{
����unsigned int j=0;
����while(1)
����{
����PORTB=j ;
����//OSTimeDly(50);
����}
����}
����void Task1()
����{
����unsigned int j=0;
����while(1)
����{
����PORTC=j ;
����//OSTimeDly(5);
����}
����}
����void Task2()
����{
����unsigned int j=0;
����while(1)
����{
����PORTD=j ;
����//OSTimeDly(5);
����}
����}
����void TaskScheduler()
����{
����while(1)
����{
����OSSched(); //�������е���
����}
����}
����int main(void)
����{
����TCN0Init();
����OSRdyTbl=0;
����OSTaskCreate(Task0,&Stack[99],0);
����OSTaskCreate(Task1,&Stack[199],1);
����OSTaskCreate(Task2,&Stack[299],2);
����OSTaskCreate(TaskScheduler,&Stack[399],OS_TASKS);
����OSStartTask();
����}
��������ƪ:ռ��ʽ�ں�(ֻ����ʱ����)
����Preemptive Multitasking
������������ʱ��Ƭ�ַ����ȷ���������ȷ�ʽ��ռ��ʽ���ں˵�ԭ���Ѿ����ֿɼ��ˡ�
���������룬ռ��ʽ�ں�����ʲô�ط�ʵ��������ȵ���?���ˣ����ڿ����������н��е��ȣ������Э��ʽ���ں����Ѿ�������;ͬʱ����Ҳ�������жϽ�������е��ȣ�������⣬�Ѿ���ʱ��Ƭ�ַ����ȷ����Ѿ������ˡ�
���������ж��ǿ���Ƕ�׵ģ�ֻ�е�����Ƕ����Ҫ����ȣ������ж�Ƕ�׷��ص����������жϵ���һ��ʱ�����ܽ���������ȡ�
����#include
����#include
����#include
����unsigned char Stack[400];
����register unsigned char OSRdyTbl asm("r2"); //�������о�����
����register unsigned char OSTaskRunningPrio asm("r3"); //�������е�����
����register unsigned char IntNum asm("r4"); //�ж�Ƕ�׼�����
����//ֻ�е��ж�Ƕ����Ϊ0���������ж�Ҫ��ʱ���������˳��ж�ʱ�������������
����register unsigned char OSCoreState asm("r16"); // ϵͳ���ı�־λ ,R16 ������û��ʹ��
����//ֻ�д���R15�ļĴ�������ֱ�Ӹ�ֵ ��LDI R16,0x01
����//0x01 �������� �л� 0x02 ���ж�Ҫ���л�
����#define OS_TASKS 3 //�趨�������������
����struct TaskCtrBlock
����{
����unsigned int OSTaskStackTop; //��������Ķ�ջ��
����unsigned int OSWaitTick; //������ʱʱ��
����} TCB[OS_TASKS 1];
����//��ֹ��������ռ��
����//register unsigned char tempR4 asm("r4");
����register unsigned char tempR5 asm("r5");
����register unsigned char tempR6 asm("r6");
����register unsigned char tempR7 asm("r7");
����register unsigned char tempR8 asm("r8");
����register unsigned char tempR9 asm("r9");
����register unsigned char tempR10 asm("r10");
����register unsigned char tempR11 asm("r11");
����register unsigned char tempR12 asm("r12");
����register unsigned char tempR13 asm("r13");
����register unsigned char tempR14 asm("r14");
����register unsigned char tempR15 asm("r15");
����//register unsigned char tempR16 asm("r16");
����register unsigned char tempR16 asm("r17");
����//��������
����void OSTaskCreate(void (*Task)(void),unsigned char *Stack,unsigned char TaskID)
����{
����unsigned char i;
����*Stack--=(unsigned int)Task>>8; //������ĵ�ַ��λѹ���ջ��
����*Stack--=(unsigned int)Task; //������ĵ�ַ��λѹ���ջ��
����*Stack--=0x00; //R1 __zero_reg__
����*Stack--=0x00; //R0 __tmp_reg__
����*Stack--=0x80;
����//SREG �������У�����ȫ���ж�
����for(i=0;i<14;i ) //�� avr-libc �е� FAQ�е� What registers are used by the C compiler?
����*Stack--=i; //�����˼Ĵ���������
����TCB[TaskID].OSTaskStackTop=(unsigned int)Stack; //���˹���ջ��ջ�������浽��ջ��������
����OSRdyTbl|=0x01<
����}
����//��ʼ�������,��������ȼ�������Ŀ�ʼ
����void OSStartTask()
����{
����OSTaskRunningPrio=OS_TASKS;
����SP=TCB[OS_TASKS].OSTaskStackTop 17;
����__asm__ __volatile__( "reti" "\n\t" );
����}
����//�����������
����void OSSched(void)
����{
����__asm__ __volatile__("LDI R16,0x01 \n\t");
����//����ж�Ҫ�������л��ı�־λ,�������������л���־λ
����__asm__ __volatile__("SEI \n\t");
����//���ж�,��Ϊ������ж�����������н���,Ҫ���½��е���ʱ���Ѿ����ж�
����//�����ж�ʱ����Ĵ����Ĵ�����ջ��ģ��һ���жϺ���ջ�����
����__asm__ __volatile__("PUSH __zero_reg__ \n\t"); //R1
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t"); //R0
����__asm__ __volatile__("IN __tmp_reg__,__SREG__ \n\t"); //����״̬�Ĵ���SREG
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t");
����__asm__ __volatile__("CLR __zero_reg__ \n\t"); //R0��������
����__asm__ __volatile__("PUSH R18 \n\t");
����__asm__ __volatile__("PUSH R19 \n\t");
����__asm__ __volatile__("PUSH R20 \n\t");
����__asm__ __volatile__("PUSH R21 \n\t");
����__asm__ __volatile__("PUSH R22 \n\t");
����__asm__ __volatile__("PUSH R23 \n\t");
����__asm__ __volatile__("PUSH R24 \n\t");
����__asm__ __volatile__("PUSH R25 \n\t");
����__asm__ __volatile__("PUSH R26 \n\t");
����__asm__ __volatile__("PUSH R27 \n\t");
����__asm__ __volatile__("PUSH R30 \n\t");
����__asm__ __volatile__("PUSH R31 \n\t");
����__asm__ __volatile__("Int_OSSched: \n\t"); //���ж�Ҫ����ȣ�ֱ�ӽ�������
����__asm__ __volatile__("SEI \n\t");
����//���ж�,��Ϊ������ж�����������н��У��Ѿ����ж�
����__asm__ __volatile__("PUSH R28 \n\t"); //R28��R29���ڽ����ڶ�ջ�ϵ�ָ��
����__asm__ __volatile__("PUSH R29 \n\t"); //��ջ���
����TCB[OSTaskRunningPrio].OSTaskStackTop=SP; //���������е�����Ķ�ջ�ױ���
����unsigned char OSNextTaskPrio; //�����ж�ջ�Ͽ����µĿռ�
����for (OSNextTaskPrio = 0; //�����������
����OSNextTaskPrio < OS_TASKS && !(OSRdyTbl & (0x01<
����OSNextTaskPrio );
����OSTaskRunningPrio = OSNextTaskPrio ;
����cli(); //������ջת��
����SP=TCB[OSTaskRunningPrio].OSTaskStackTop;
����sei();
����//�����ж�ʱ�ĳ�ջ����
����__asm__ __volatile__("POP R29 \n\t");
����__asm__ __volatile__("POP R28 \n\t");
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("POP R30 \n\t");
����__asm__ __volatile__("POP R27 \n\t");
����__asm__ __volatile__("POP R26 \n\t");
����__asm__ __volatile__("POP R25 \n\t");
����__asm__ __volatile__("POP R24 \n\t");
����__asm__ __volatile__("POP R23 \n\t");
����__asm__ __volatile__("POP R22 \n\t");
����__asm__ __volatile__("POP R21 \n\t");
����__asm__ __volatile__("POP R20 \n\t");
����__asm__ __volatile__("POP R19 \n\t");
����__asm__ __volatile__("POP R18 \n\t");
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //SERG ��ջ���ָ�
����__asm__ __volatile__("OUT __SREG__,__tmp_reg__ \n\t"); //
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //R0 ��ջ
����__asm__ __volatile__("POP __zero_reg__ \n\t"); //R1 ��ջ
����//�ж�ʱ��ջ���
����__asm__ __volatile__("CLI \n\t"); //���ж�
����__asm__ __volatile__("SBRC R16,1 \n\t"); //SBRC���Ĵ���λΪ0��������һ��ָ��
����//������ڵ���ʱ���Ƿ����ж�Ҫ��������� 0x02���ж�Ҫ����ȵı�־λ
����__asm__ __volatile__("RJMP OSSched \n\t"); //���µ���
����__asm__ __volatile__("LDI R16,0x00 \n\t");
����//����ж�Ҫ�������л��ı�־λ,������������л���־λ
����__asm__ __volatile__("RETI \n\t"); //���ز����ж�
����}
����//���ж��˳������е���
����void IntSwitch(void)
����{
����//���ж���Ƕ�ף�����û�����л�����Ĺ����У�ֱ�ӽ��������л�
����if(OSCoreState == 0x02 && IntNum==0)
����{
����//�����ж�ʱ���Ѿ�������SREG��R0,R1,R18~R27,R30,R31
����__asm__ __volatile__("POP R31 \n\t"); //ȥ��������ӳ������ջ��PC
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("LDI R16,0x01 \n\t");
����//����ж�Ҫ�������л��ı�־λ,�������������л���־λ
����__asm__ __volatile__("RJMP Int_OSSched \n\t"); //���µ���
����}
����}
����// ������ʱ
����void OSTimeDly(unsigned int ticks)
����{
����if(ticks) //����ʱ��Ч
����{
����OSRdyTbl &= ~(0x01<
����TCB[OSTaskRunningPrio].OSWaitTick=ticks;
����OSSched(); //���µ���
����}
����}
����void TCN0Init(void) // ��ʱ��0
����{
����TCCR0 = 0;
����TCCR0 |= (1<
����TIMSK |= (1<
����TCNT0 = 100; // �ü�����ʼֵ
����}
����SIGNAL(SIG_OVERFLOW0)
����{
����IntNum ; //�ж�Ƕ�� 1
����sei(); //���ж��У��ؿ��ж�
����unsigned char i,j=0;
����for(i=0;i
����{
����if(TCB[i].OSWaitTick)
����{
����TCB[i].OSWaitTick--;
����if(TCB[i].OSWaitTick==0) //������ʱ�ӵ�ʱ,�������ɶ�ʱ����ʱ�Ĳ���
����{
����OSRdyTbl |= (0x01<
����OSCoreState|=0x02; //Ҫ�������л��ı�־λ
����}
����}
����}
����TCNT0=100;
����cli();
����IntNum--; //�ж�Ƕ��-1
����IntSwitch(); //�����������
����}
����void Task0()
����{
����unsigned int j=0;
����while(1)
����{
����PORTB=j ;
����OSTimeDly(50);
����}
����}
����void Task1()
����{
����unsigned int j=0;
����while(1)
����{
����PORTC=j ;
����OSTimeDly(20);
����}
����}
����void Task2()
����{
����unsigned int j=0;
����while(1)
����{
����PORTD=j ;
����OSTimeDly(5);
����}
����}
����void TaskScheduler()
����{
����OSSched();
����while(1)
����{
����//OSSched(); //�������е���
����}
����}
����int main(void)
����{
����TCN0Init();
����OSRdyTbl=0;
����IntNum=0;
����OSTaskCreate(Task0,&Stack[99],0);
����OSTaskCreate(Task1,&Stack[199],1);
����OSTaskCreate(Task2,&Stack[299],2);
����OSTaskCreate(TaskScheduler,&Stack[399],OS_TASKS);
����OSStartTask();
����}
�����ڰ�ƪ:ռ��ʽ�ں�(���Ƶķ���)
���������ǰ�����ᵽ��ռ��ʽ�ں˺�Э��ʽ�ں������һ�𣬺����׾Ϳ��Եõ�һ�����ܽ�Ϊ���Ƶ�ռ��ʽ�ںˣ����Ĺ����У�
����1,����ͻָ�����
����2,������ʱ
����3,�ź���(���������ͺͶ�ռ��)
�������⣬�ڱ����У��ڸ��������м����˴Ӵ��ڷ�������״̬�Ĺ��ܡ�
����#include
����#include
����#include
����unsigned char Stack[400];
����register unsigned char OSRdyTbl asm("r2"); //�������о�����
����register unsigned char OSTaskRunningPrio asm("r3"); //�������е�����
����register unsigned char IntNum asm("r4"); //�ж�Ƕ�׼�����
����//ֻ�е��ж�Ƕ����Ϊ0���������ж�Ҫ��ʱ���������˳��ж�ʱ�������������
����register unsigned char OSCoreState asm("r16"); // ϵͳ���ı�־λ ,R16 ������û��ʹ��
����//ֻ�д���R15�ļĴ�������ֱ�Ӹ�ֵ ��LDI R16,0x01
����//0x01 �������� �л� 0x02 ���ж�Ҫ���л�
����#define OS_TASKS 3 //�趨�������������
����struct TaskCtrBlock
����{
����unsigned int OSTaskStackTop; //��������Ķ�ջ��
����unsigned int OSWaitTick; //������ʱʱ��
����} TCB[OS_TASKS 1];
����//��ֹ��������ռ��
����//register unsigned char tempR4 asm("r4");
����register unsigned char tempR5 asm("r5");
����register unsigned char tempR6 asm("r6");
����register unsigned char tempR7 asm("r7");
����register unsigned char tempR8 asm("r8");
����register unsigned char tempR9 asm("r9");
����register unsigned char tempR10 asm("r10");
����register unsigned char tempR11 asm("r11");
����register unsigned char tempR12 asm("r12");
����register unsigned char tempR13 asm("r13");
����register unsigned char tempR14 asm("r14");
����register unsigned char tempR15 asm("r15");
����//register unsigned char tempR16 asm("r16");
����register unsigned char tempR16 asm("r17");
����//��������
����void OSTaskCreate(void (*Task)(void),unsigned char *Stack,unsigned char TaskID)
����{
����unsigned char i;
����*Stack--=(unsigned int)Task>>8; //������ĵ�ַ��λѹ���ջ��
����*Stack--=(unsigned int)Task; //������ĵ�ַ��λѹ���ջ��
����*Stack--=0x00; //R1 __zero_reg__
����*Stack--=0x00; //R0 __tmp_reg__
����*Stack--=0x80;
����//SREG �������У�����ȫ���ж�
����for(i=0;i<14;i ) //�� avr-libc �е� FAQ�е� What registers are used by the C compiler?
����*Stack--=i; //�����˼Ĵ���������
����TCB[TaskID].OSTaskStackTop=(unsigned int)Stack; //���˹���ջ��ջ�������浽��ջ��������
����OSRdyTbl|=0x01<
����}
����//��ʼ�������,��������ȼ�������Ŀ�ʼ
����void OSStartTask()
����{
����OSTaskRunningPrio=OS_TASKS;
����SP=TCB[OS_TASKS].OSTaskStackTop 17;
����__asm__ __volatile__( "reti" "\n\t" );
����}
����//�����������
����void OSSched(void)
����{
����__asm__ __volatile__("LDI R16,0x01 \n\t");
����//����ж�Ҫ�������л��ı�־λ,�������������л���־λ
����__asm__ __volatile__("SEI \n\t");
����//���ж�,��Ϊ������ж�����������н���,Ҫ���½��е���ʱ���Ѿ����ж�
����// �����ж�ʱ����Ĵ����Ĵ�����ջ��ģ��һ���жϺ���ջ�����
����__asm__ __volatile__("PUSH __zero_reg__ \n\t"); //R1
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t"); //R0
����__asm__ __volatile__("IN __tmp_reg__,__SREG__ \n\t"); //����״̬�Ĵ���SREG
����__asm__ __volatile__("PUSH __tmp_reg__ \n\t");
����__asm__ __volatile__("CLR __zero_reg__ \n\t"); //R0��������
����__asm__ __volatile__("PUSH R18 \n\t");
����__asm__ __volatile__("PUSH R19 \n\t");
����__asm__ __volatile__("PUSH R20 \n\t");
����__asm__ __volatile__("PUSH R21 \n\t");
����__asm__ __volatile__("PUSH R22 \n\t");
����__asm__ __volatile__("PUSH R23 \n\t");
����__asm__ __volatile__("PUSH R24 \n\t");
����__asm__ __volatile__("PUSH R25 \n\t");
����__asm__ __volatile__("PUSH R26 \n\t");
����__asm__ __volatile__("PUSH R27 \n\t");
����__asm__ __volatile__("PUSH R30 \n\t");
����__asm__ __volatile__("PUSH R31 \n\t");
����__asm__ __volatile__("Int_OSSched: \n\t"); //���ж�Ҫ����ȣ�ֱ�ӽ�������
����__asm__ __volatile__("SEI \n\t");
����//���ж�,��Ϊ������ж�����������н��У��Ѿ����ж�
����__asm__ __volatile__("PUSH R28 \n\t"); //R28��R29���ڽ����ڶ�ջ�ϵ�ָ��
����__asm__ __volatile__("PUSH R29 \n\t"); //��ջ���
����TCB[OSTaskRunningPrio].OSTaskStackTop=SP; //���������е�����Ķ�ջ�ױ���
����unsigned char OSNextTaskPrio; //�����ж�ջ�Ͽ����µĿռ�
����for (OSNextTaskPrio = 0; //�����������
����OSNextTaskPrio < OS_TASKS && !(OSRdyTbl & (0x01<
����OSNextTaskPrio );
����OSTaskRunningPrio = OSNextTaskPrio ;
����cli(); //������ջת��
����SP=TCB[OSTaskRunningPrio].OSTaskStackTop;
����sei();
����//�����ж�ʱ�ĳ�ջ����
����__asm__ __volatile__("POP R29 \n\t");
����__asm__ __volatile__("POP R28 \n\t");
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("POP R30 \n\t");
����__asm__ __volatile__("POP R27 \n\t");
����__asm__ __volatile__("POP R26 \n\t");
����__asm__ __volatile__("POP R25 \n\t");
����__asm__ __volatile__("POP R24 \n\t");
����__asm__ __volatile__("POP R23 \n\t");
����__asm__ __volatile__("POP R22 \n\t");
����__asm__ __volatile__("POP R21 \n\t");
����__asm__ __volatile__("POP R20 \n\t");
����__asm__ __volatile__("POP R19 \n\t");
����__asm__ __volatile__("POP R18 \n\t");
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //SERG ��ջ���ָ�
����__asm__ __volatile__("OUT __SREG__,__tmp_reg__ \n\t"); //
����__asm__ __volatile__("POP __tmp_reg__ \n\t"); //R0 ��ջ
����__asm__ __volatile__("POP __zero_reg__ \n\t"); //R1 ��ջ
����//�ж�ʱ��ջ���
����__asm__ __volatile__("CLI \n\t"); //���ж�
����__asm__ __volatile__("SBRC R16,1 \n\t"); //SBRC���Ĵ���λΪ0��������һ��ָ��
����//������ڵ���ʱ���Ƿ����ж�Ҫ��������� 0x02���ж�Ҫ����ȵı�־λ
����__asm__ __volatile__("RJMP OSSched \n\t"); //���µ���
����__asm__ __volatile__("LDI R16,0x00 \n\t");
����//����ж�Ҫ�������л��ı�־λ,������������л���־λ
����__asm__ __volatile__("RETI \n\t"); //���ز����ж�
����}
����//���ж��˳������е���
����void IntSwitch(void)
����{
����//���ж���Ƕ�ף�����û�����л�����Ĺ����У�ֱ�ӽ��������л�
����if(OSCoreState == 0x02 && IntNum==0)
����{
����//�����ж�ʱ���Ѿ�������SREG��R0,R1,R18~R27,R30,R31
����__asm__ __volatile__("POP R31 \n\t"); //ȥ��������ӳ������ջ��PC
����__asm__ __volatile__("POP R31 \n\t");
����__asm__ __volatile__("LDI R16,0x01 \n\t");
����//����ж�Ҫ�������л��ı�־λ,�������������л���־λ
����__asm__ __volatile__("RJMP Int_OSSched \n\t"); //���µ���
����}
����}
����////////////////////////////////////////////������
����//��������
����void OSTaskSuspend(unsigned char prio)
����{
����TCB[prio].OSWaitTick=0;
����OSRdyTbl &= ~(0x01<
����if(OSTaskRunningPrio==prio) //��Ҫ���������Ϊ��ǰ����
����OSSched(); //���µ���
����}
����//�ָ����� �����ñ�OSTaskSuspend�� OSTimeDly��ͣ������ָ�
����void OSTaskResume(unsigned char prio)
����{
����OSRdyTbl |= 0x01<
����TCB[prio].OSWaitTick=0; //��ʱ���ʱ��Ϊ0,��ʱ
����if(OSTaskRunningPrio>prio) //��Ҫ��ǰ��������ȼ���������λ����������ȼ�
����OSSched(); //���µ��� //���µ���
����}
����// ������ʱ
����void OSTimeDly(unsigned int ticks)
����{
����if(ticks) //����ʱ��Ч
����{
����OSRdyTbl &= ~(0x01<
����TCB[OSTaskRunningPrio].OSWaitTick=ticks;
����OSSched(); //���µ���
����}
����}
����//�ź���
����struct SemBlk
����{
����unsigned char OSEventType; //�ͺ� 0,�ź�����ռ��;1�ź���������
����unsigned char OSEventState; //״̬ 0,������;1,����
����unsigned char OSTaskPendTbl; //�ȴ��ź����������б�
����} Sem[10];
����//��ʼ���ź���
����void OSSemCreat(unsigned char Index,unsigned char Type)
����{
����Sem[Index].OSEventType=Type; //�ͺ� 0,�ź�����ռ��;1�ź���������
����Sem[Index].OSTaskPendTbl=0;
����Sem[Index].OSEventState=0;
����}
����//����ȴ��ź���,����
����//��Timeout==0xffffʱ��Ϊ������ʱ
����unsigned char OSTaskSemPend(unsigned char Index,unsigned int Timeout)
����{
����//unsigned char i=0;
����if(Sem[Index].OSEventState) //�ź�����Ч
����{
����if(Sem[Index].OSEventType==0) //���Ϊ��ռ��
����Sem[Index].OSEventState = 0x00; //�ź�������ռ��������
����}
����else
����{ //�����źŵ�����ȴ���
����Sem[Index].OSTaskPendTbl |= 0x01<
����TCB[OSTaskRunningPrio].OSWaitTick=Timeout; //����ʱΪ0�������޵ȴ�
����OSRdyTbl &= ~(0x01<
����OSSched(); //���µ���
����if(TCB[OSTaskRunningPrio].OSWaitTick==0 ) //��ʱ��δ���õ���Դ
����return 0;
����}
����return 1;
����}
����//����һ���ź��������Դ�������жϷ���
����void OSSemPost(unsigned char Index)
����{
����if(Sem[Index].OSEventType) //��Ҫ����ź����ǹ�����
����{
����Sem[Index].OSEventState=0x01; //ʹ�ź�����Ч
����OSRdyTbl |=Sem [Index].OSTaskPendTbl; //ʹ�ڵȴ����źŵ������������
����Sem[Index].OSTaskPendTbl=0; //������еȴ����źŵĵȴ�����
����}
����else //��Ҫ����ź���Ϊ��ռ��
����{
����unsigned char i;
����for (i = 0; i < OS_TASKS && !(Sem[Index].OSTaskPendTbl & (0x01<
����if(i < OS_TASKS) //�����������Ҫ
����{
����Sem[Index].OSTaskPendTbl &= ~(0x01<
����OSRdyTbl |= 0x01<
����}
����else
����{
����Sem[Index].OSEventState =1; //ʹ�ź�����Ч
����}
����}
����}
����//��������һ���ź����������е���
����void OSTaskSemPost(unsigned char Index)
����{
����OSSemPost(Index);
����OSSched();
����}
����//���һ���ź���,ֻ�Թ����͵����á�
����//���ڶ�ռ�͵��ź�����������ռ�ú󣬾ͽ��ò��������ˡ�
����void OSSemClean(unsigned char Index)
����{
����Sem[Index].OSEventState =0; //Ҫ����ź�����Ч
����}
����void TCN0Init(void) // ��ʱ��0
����{
����TCCR0 = 0;
����TCCR0 |= (1<
����TIMSK |= (1<
����TCNT0 = 100; // �ü�����ʼֵ
����}
����SIGNAL(SIG_OVERFLOW0)
����{
����IntNum ; //�ж�Ƕ�� 1
����sei(); //���ж��У��ؿ��ж�
����unsigned char i;
����for(i=0;i
����{
����if(TCB[i].OSWaitTick && TCB[i].OSWaitTick!=0xffff)
����{
����TCB[i].OSWaitTick--;
����if(TCB[i].OSWaitTick==0) //������ʱ�ӵ�ʱ,�������ɶ�ʱ����ʱ�Ĳ���
����{
����OSRdyTbl |= (0x01<
����OSCoreState|=0x02; //Ҫ�������л��ı�־λ
����}
����}
����}
����TCNT0=100;
����cli();
����IntNum--; //�ж�Ƕ��-1
����IntSwitch(); //�����������
����}
����unsigned char __attribute__ ((progmem)) proStrA[]="Task ";
����unsigned char strA[20];
����SIGNAL(SIG_UART_RECV) //���ڽ����ж�
����{
����strA[0]=UDR;
����}
����/////////////////////////////////////���ڷ���
����unsigned char *pstr_UART_Send;
����unsigned int nUART_Sending=0;
����void UART_Send(unsigned char *Res,unsigned int Len) //�����ַ�������
����{
����if(Len>0)
����{
����pstr_UART_Send=Res; //�����ִ���ָ��
����nUART_Sending=Len; //�����ִ��ĳ���
����UCSRB=0xB8; //�����ж�ʹ��
����}
����}
����//SIGNAL ���ж��ڼ䣬�����жϽ�ֹ
����SIGNAL(SIG_UART_DATA) //���ڷ��������ж�
����{
����IntNum ; //�ж�Ƕ�� 1,�������ж�
����if(nUART_Sending) //���δ����
����{
����UDR=*pstr_UART_Send; //�����ֽ�
����pstr_UART_Send ; //�����ִ���ָ���1
����nUART_Sending--; //�ȴ����͵��ִ�����1
����}
����if(nUART_Sending==0) //���Ѿ�������
����{
����OSSemPost(0);
����OSCoreState|=0x02; //Ҫ�������л��ı�־λ
����UCSRB=0x98;
����}
����cli(); //�ط����ж�
����IntNum--;
����IntSwitch(); //�����������
����}
����void UARTInit() //��ʼ������
����{
����#define fosc 8000000 //����8 MHZ UBRRL=(fosc/16/(baud 1))%6;
����#define baud 9600 //������
����OSCCAL=0x97; //���ڲ�����У��ֵ���ӱ�����ж���
����//UCSRB=(1<
����UCSRB=0x98;
����//UCSRB=0x08;
����UBRRL=(fosc/16/(baud 1))%6;
����UBRRH=(fosc/16/(baud 1))/256;
����UCSRC=(1<
����UCSRB=0xB8;
����UDR=0;
����}
����//��ӡunsigned int ���ַ����� 00000
����void strPUT_uInt(unsigned char *Des,unsigned int i)
����{
����unsigned char j;
����Des=Des 4;
����for(j=0;j<5;j )
����{
����*Des=i ��0��;
����i=i/10;
����Des--;
����}
����}
����void strPUT_Star(unsigned char *Des,unsigned char i)
����{
����unsigned char j;
����for(j=0;j
����{
����*Des =��*��;
����}
����*Des =13;
����}
����unsigned int strPUT_TaskState(unsigned char *Des,
����unsigned char TaskID,
����unsigned char Num)
����{
����//unsigned int i=0;
����*(Des 4)=��0�� TaskID;
����strPUT_uInt(Des 6,Num);
����strPUT_Star(Des 12,TaskID);
����return 12 TaskID 1;
����}
����void Task0()
����{
����unsigned int j=0;
����while(1)
����{
����PORTB=j ;
����if(OSTaskSemPend(0,0xffff))
����{
����unsigned int m;
����m=strPUT_TaskState(strA,OSTaskRunningPrio,j);
����UART_Send(strA,m);
����}
����OSTimeDly(200);
����}
����}
����void Task1()
����{
����unsigned int j=0;
����while(1)
����{
����PORTC=j ;
����if(OSTaskSemPend(0,0xffff))
����{
����unsigned int m;
����m=strPUT_TaskState(strA,OSTaskRunningPrio,j);
����UART_Send(strA,m);
����}
����OSTimeDly(100);
����}
����}
����void Task2()
����{
����unsigned int j=0;
����while(1)
����{
����if(OSTaskSemPend(0,0xffff))
����{
����unsigned int m;
����m=strPUT_TaskState(strA,OSTaskRunningPrio,j);
����UART_Send(strA,m);
����}
����PORTD=j ;
����OSTimeDly(50);
����}
����}
����void TaskScheduler()
����{
����OSSched();
����while(1)
����{
����}
����}
����int main(void)
����{
����strlcpy_P(strA,proStrA,20);
����UARTInit();
����TCN0Init();
����OSRdyTbl=0;
����IntNum=0;
����OSTaskCreate(Task0,&Stack[99],0);
����OSTaskCreate(Task1,&Stack[199],1);
����OSTaskCreate(Task2,&Stack[299],2);
����OSTaskCreate(TaskScheduler,&Stack[399],OS_TASKS);
����OSStartTask();
}

## ������
���������е����ӣ���������WinAVR�� Proteus���Է���ɹ���һ�����ܴ���ĳЩ�����ȱ��,��Ϊ������ʱ���ѹ������û�н�һ�����ҡ�
�����������ţ����ͨ��ѧϰ����һ�����˽�һ���ں˵ľ���ʵ����ʽ���������ƣ���������д��һ�������Լ����ںˡ�
����������һ���Ļ���֪ʶ���ٻ�ͷ���� UCOSII��small rots51�ȣ����ܻ��и������ᣬ�Խ�һ���˽�Ƕ��ʽϵͳ�Ͳ���ϵͳ����������������ϣ�������ܰ������������һ�㡣
����ϣ������ܹ�����Լ������������һ���н׶��Ե��ܽᣬ�������ܵز��ϸĽ���
����ţ����˵���������ܹ����ø�Զ������Ϊվ�ھ��˵ļ���ϡ���
����ϣ����Ҷ��ܳ�һ�������ƶ����ǵ�Ƕ��ʽ����ҵ�Ľ�һ����չ��
����2006��1��14�� ϣ��ͬ�ж�ཻ����


----
**������Դ��** 
>ԭ�� zhxianbin@163.com

**�޸ļ�¼��**
> 2017-04-02  �״η���

**�ο����ϣ�**
> todo
# assignment queue
#include "board.h"
#include "FreeRTOS.h"
#include "task.h"
#include "queue.h"
#include "croutine.h"
static void prvSetupHardware(void)
{
SystemCoreClockUpdate();
Board_Init();
/* Initial LED0 state is off */
Board_LED_Set(0, false);
Board_LED_Set(1, false);
Board_LED_Set(2, false);
}
int sendok;
/* LED1 toggle thread */
static void vSenderTask(void *pvParameters)
{
int32_t lValueToSend;
int32_t xStatus;
lValueToSend = ( int32_t ) pvParameters;
int sendok;
float RAND_MAX;
while (1)
{
if (sendok == 1);
{
Board_LED_Set(0, false);
float i = rand ();
float r = ((float)i)/((float)RAND_MAX);
vTaskDelay(configTICK_RATE_HZ);
}
}
}static void vReceiverTask( void *pvParameters )
{
int32_t lReceivedValue;
int32_t xStatus;
const TickType_t xTicksToWait = pdMS_TO_TICKS( 100 );
while (1)
{
if( uxQueueMessagesWaiting( xQueue ) != 0 )
{
Board_LED_Set(0, false);
}
xStatus = xQueueReceive( xQueue, &lReceivedValue, xTicksToWait );
}
}
void vTimerTask(void *pvParameters)
{
while(1)
{
if (sendok == 1)
{
vTaskDelay(40000);
}
else if (sendok == 0)
{
vTaskDelay(300000);
}
}
}
int main( void )
{
xQueue = xQueueCreate( 5, sizeof( int32_t ) );
if( xQueue != NULL )
{while (1);
xTaskCreate( vSenderTask, "Sender1", 1000, ( void * ) 100, 1, NULL );
xTaskCreate( vSenderTask, "Sender2", 1000, ( void * ) 200, 1, NULL );
xTaskCreate( vReceiverTask, "Receiver", 1000, NULL, 2, NULL );
vTaskStartScheduler();
w
}
}
/* UART (or output) thread */
static void vUARTTask(void *pvParameters) {
int tickCnt = 0;
while (1) {
DEBUGOUT("Tick: %d\r\n", tickCnt);
tickCnt++;
/* About a 1s delay here */
vTaskDelay(configTICK_RATE_HZ);
}
}

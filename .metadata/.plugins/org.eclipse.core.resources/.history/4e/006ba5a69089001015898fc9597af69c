/* USER CODE BEGIN Header */
/**
  ******************************************************************************
  * @file           : main.c
  * @brief          : Main program body
  ******************************************************************************
  * @attention
  *
  * Copyright (c) 2025 STMicroelectronics.
  * All rights reserved.
  *
  * This software is licensed under terms that can be found in the LICENSE file
  * in the root directory of this software component.
  * If no LICENSE file comes with this software, it is provided AS-IS.
  *
  ******************************************************************************
  */
/* USER CODE END Header */
/* Includes ------------------------------------------------------------------*/
#include "main.h"
#include "adc.h"
#include "dma.h"
#include "usart.h"
#include "gpio.h"
#include "string.h"
#include "stdio.h"

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */

/* USER CODE END Includes */

/* Private typedef -----------------------------------------------------------*/
/* USER CODE BEGIN PTD */

/* USER CODE END PTD */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */

/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/

/* USER CODE BEGIN PV */
#define ADC_NUM_CHANNELS   8
#define ADC_BUF_LEN        (ADC_NUM_CHANNELS * 2)

static volatile uint16_t adc_buf[ADC_BUF_LEN];
static volatile uint8_t  half_ready = 0;
static volatile uint8_t  full_ready = 0;

static char uart_line[160];
char msg[32];
volatile uint32_t adc_val = 0;
/* USER CODE END PV */

/* Private function prototypes -----------------------------------------------*/
void SystemClock_Config(void);
static void MPU_Config(void);
/* USER CODE BEGIN PFP */

/* USER CODE END PFP */

/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */
static void print_frame_over_uart_half(const uint16_t *p, const char *tag)
{
  float v_half[4];
  for (int i = 0; i < 4; i++)
	  {
	    v_half[i] = (p[i] * 3.3f) / 4095.0f;   // Convert to voltage
	  }
//	  snprintf(msg, sizeof(msg), " Vin = %.2f V\r\n", voltage);
  int len = snprintf(uart_line, sizeof(uart_line),
                     "%s: \n\r " "ADC1_CH10 = 0x%08X Vin = %.2fV\n\r " "ADC1_CH4 = 0x%08X Vin = %.2fV\n\r " "ADC1_CH3 = 0x%08X Vin = %.2fV\n\r " "ADC1_CH13 = 0x%08X Vin = %.2fV\r\n",
                     tag,
					 p[0], v_half[0], p[1], v_half[1], p[2], v_half[2], p[3], v_half[3]);
  if (len > 0)
  {
    HAL_UART_Transmit(&huart3, (uint8_t*)uart_line, (uint16_t)len, 100);
  }
}

static void print_frame_over_uart_full(const uint16_t *p, const char *tag)
{
	  float v_full[8];
	  for (int i = 4; i < 8; i++)
		  {
		    v_full[i] = (p[i] * 3.3f) / 4095.0f;   // Convert to voltage
		  }
  int len = snprintf(uart_line, sizeof(uart_line),
		             "%s: \n\r " "ADC1_CH12 = 0x%08X Vin = %.2fV\n\r " "ADC1_CH0 = 0x%08X Vin = %.2fV\n\r " "ADC1_CH9 = 0x%08X Vin = %.2fV\n\r " "ADC1_CH5 = 0x%08X Vin = %.2fV\r\n",
                     tag,
                     p[4], v_full[4], p[5], v_full[5], p[6], v_full[6], p[7], v_full[7]);
  if (len > 0)
  {
    HAL_UART_Transmit(&huart3, (uint8_t*)uart_line, (uint16_t)len, 100);
  }
}
/* USER CODE END 0 */

/**
  * @brief  The application entry point.
  * @retval int
  */
int main(void)
{

  /* USER CODE BEGIN 1 */

  /* USER CODE END 1 */

  /* MPU Configuration--------------------------------------------------------*/
  MPU_Config();

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  MX_DMA_Init();
  MX_ADC1_Init();
  MX_USART3_UART_Init();
  /* USER CODE BEGIN 2 */
  HAL_ADC_Start_DMA(&hadc1, (uint32_t*)adc_buf, ADC_BUF_LEN);
  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */

//	  adc1 pa3 pc0 pc3 pa7
//	  adc2 pb1 pc2 pa0 pb0
//	  while (HAL_ADC_PollForConversion(&hadc1, 100) != HAL_OK) {}
//	  adc_val = HAL_ADC_GetValue(&hadc1);
//	  msg[32]
//	  HAL_UART_Transmit(&huart3, (uint8_t*)adc_val, strlen(adc_val), HAL_MAX_DELAY);
//
//	  char m[100] = "\r\n-------------------------------------------------\n\r";
//	  HAL_UART_Transmit(&huart3, (uint8_t*)m, strlen(m), HAL_MAX_DELAY);

//	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_7, GPIO_PIN_SET);
//	  HAL_Delay(200);
//	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_7, GPIO_PIN_RESET);
//	  HAL_Delay(200);
//
//	  if (half_ready)
//	      {
//	        half_ready = 0;
//	        HAL_GPIO_WritePin(GPIOB, GPIO_PIN_7, GPIO_PIN_SET);
//	        print_frame_over_uart(&adc_buf[0],  "[HALF]");
//	      }
//
//	      if (full_ready)
//	      {
//	        full_ready = 0;
//	        HAL_GPIO_WritePin(GPIOB, GPIO_PIN_7, GPIO_PIN_RESET);
//	        print_frame_over_uart(&adc_buf[ADC_NUM_CHANNELS], "[FULL]");
//	      }
//
//	   HAL_Delay(400);
  }
  /* USER CODE END 3 */
}

/**
  * @brief System Clock Configuration
  * @retval None
  */
void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

  /** Configure the main internal regulator output voltage
  */
  __HAL_RCC_PWR_CLK_ENABLE();
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE3);

  /** Initializes the RCC Oscillators according to the specified parameters
  * in the RCC_OscInitTypeDef structure.
  */
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }

  /** Initializes the CPU, AHB and APB buses clocks
  */
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1|RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_HSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)
  {
    Error_Handler();
  }
}

/* USER CODE BEGIN 4 */
void HAL_ADC_ConvHalfCpltCallback(ADC_HandleTypeDef* hadc)
{
  if (hadc->Instance == ADC1)
  {
      half_ready = 0;
      HAL_GPIO_WritePin(GPIOB, GPIO_PIN_7, GPIO_PIN_SET);
      print_frame_over_uart_half(&adc_buf[0],  "[HALF]");
      HAL_Delay(1000);
  }
}

void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc)
{
  if (hadc->Instance == ADC1)
  {
	  full_ready = 0;
	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_7, GPIO_PIN_RESET);
	  print_frame_over_uart_full(&adc_buf[ADC_NUM_CHANNELS], "[FULL]");
	  HAL_Delay(1000);
  }
}

void displayHEX(uint32_t value){
	char buffer[20];

	uint16_t val = (uint16_t)(value & 0xFFFF);
	sprintf(buffer, "0x%08X", val);

	HAL_UART_Transmit(&huart3, (uint8_t*)buffer, strlen(buffer), HAL_MAX_DELAY);
//	HAL_UART_Transmit(&huart3, (uint8_t*)"\r\n", 2, HAL_MAX_DELAY);
}
/* USER CODE END 4 */

 /* MPU Configuration */

void MPU_Config(void)
{
  MPU_Region_InitTypeDef MPU_InitStruct = {0};

  /* Disables the MPU */
  HAL_MPU_Disable();

  /** Initializes and configures the Region and the memory to be protected
  */
  MPU_InitStruct.Enable = MPU_REGION_ENABLE;
  MPU_InitStruct.Number = MPU_REGION_NUMBER0;
  MPU_InitStruct.BaseAddress = 0x0;
  MPU_InitStruct.Size = MPU_REGION_SIZE_4GB;
  MPU_InitStruct.SubRegionDisable = 0x87;
  MPU_InitStruct.TypeExtField = MPU_TEX_LEVEL0;
  MPU_InitStruct.AccessPermission = MPU_REGION_NO_ACCESS;
  MPU_InitStruct.DisableExec = MPU_INSTRUCTION_ACCESS_DISABLE;
  MPU_InitStruct.IsShareable = MPU_ACCESS_SHAREABLE;
  MPU_InitStruct.IsCacheable = MPU_ACCESS_NOT_CACHEABLE;
  MPU_InitStruct.IsBufferable = MPU_ACCESS_NOT_BUFFERABLE;

  HAL_MPU_ConfigRegion(&MPU_InitStruct);
  /* Enables the MPU */
  HAL_MPU_Enable(MPU_PRIVILEGED_DEFAULT);

}

/**
  * @brief  This function is executed in case of error occurrence.
  * @retval None
  */
void Error_Handler(void)
{
  /* USER CODE BEGIN Error_Handler_Debug */
  /* User can add his own implementation to report the HAL error return state */
  __disable_irq();
  while (1)
  {
  }
  /* USER CODE END Error_Handler_Debug */
}
#ifdef USE_FULL_ASSERT
/**
  * @brief  Reports the name of the source file and the source line number
  *         where the assert_param error has occurred.
  * @param  file: pointer to the source file name
  * @param  line: assert_param error line source number
  * @retval None
  */
void assert_failed(uint8_t *file, uint32_t line)
{
  /* USER CODE BEGIN 6 */
  /* User can add his own implementation to report the file name and line number,
     ex: printf("Wrong parameters value: file %s on line %d\r\n", file, line) */
  /* USER CODE END 6 */
}
#endif /* USE_FULL_ASSERT */

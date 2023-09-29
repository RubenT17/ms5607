# MS5607
Library for MS5607 altimeter sensor

https://www.parallax.com/product/altimeter-module-ms5607/


## ✒️ &nbsp; Author 
* **Rubén Torres Bermúdez** - [RubenT17](https://github.com/RubenT17)


## ⚙️ &nbsp; How to use

```
#include "ms5607.h"


typedef struct
{
	uint16_t calibration[5];
	float  temp;
	float pressure;
	float altitude;
} altimeter_t;

altimeter_t altimeter = {0};

/**
 * Read calibration from MS5607 altimeter
 * @return HAL status
 */
inline HAL_StatusTypeDef aocs_config_altimeter()
{
	HAL_StatusTypeDef err = ms5607_reset();
	if (err != HAL_OK)	return err;
	HAL_Delay(10);

	err = ms5607_readCalibration(altimeter.calibration);
	if (err != HAL_OK)	return err;

	return HAL_OK;
}

/**
 * Get altitude, pressure and temperature from MS5607 altimeter
 * @return HAL status
 */
inline HAL_StatusTypeDef aocs_get_altimeter()
{
	if(ms5607_getTempPressure(MS5607_ADC_4096, altimeter.calibration, &altimeter.temp, &altimeter.pressure) != HAL_OK)	return HAL_ERROR;
	altimeter.altitude = ms5607_getAltitude(altimeter.pressure);
	return HAL_OK;
}
```

## ❓ &nbsp; Where to ask questions 

| Type                            | Platforms                               |
| ------------------------------- | --------------------------------------- |
| 🚨 **Bug Reports**              | [GitHub Issue Tracker](https://github.com/RubenT17/ms5607/issues)                 |
| 🎁 **Feature Requests & Ideas** | [GitHub Issue Tracker](https://github.com/RubenT17/ms5607/issues)                 |


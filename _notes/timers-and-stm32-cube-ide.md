---
title: Timers and STM32 Cube IDE
---
<!--[[University]]--->
<!--[[Electronics]]--->
<!--[[Code]]--->

<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

#### Timers

$$f_{timer} = \frac{f_{clock}}{(ARR + 1)\cdot(PSC + 1)}$$

where $$ARR$$ is the counter period and $$PSC$$ is the prescaler.

Example: 

$$f_{timer} =\frac{96MHz}{(999+1)\cdot(95+1)}=\frac{96 000 000 Hz}{1000 \cdot 96} = 1000 Hz$$

$$T = \frac{1}{1000Hz} = 0.001s = 1ms$$

Then: `HAL_TIM_Base_Start(&htim1);` or `HAL_TIM_Base_Start_IT(&htim1);`

Accessing the counter period (autoreload): `__HAL_TIM_GET_AUTORELOAD(&htim1);`

Changing the counter period: `__HAL_TIM_SET_AUTORELOAD(&htim1, new_value);`

In the case of interrupts, the callback function is:

```c
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim) {
  if (htim->Instance == TIM1) { 
    // do something
  }
}
```

***

#### Pulse-Width Modulation (PWM):

$$duty\;cycle = 100\% \cdot \frac{pulse}{ARR + 1}$$

Example:

$$duty\;cycle = 100\% \cdot \frac{500}{999 + 1}=50\%$$

Then: `HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_1);`

Accessing the pulse value (CRR): `__HAL_TIM_GET_COMPARE(&htim1, TIM_CHANNEL_1);`

Changing the pulse value: `__HAL_TIM_SET_COMPARE(&htim1, TIM_CHANNEL_3, new_value);`

---

#### Rotary encoders

Disable all channels, set *combined channels* to *encoder mode*, then set the timer in the blocking mode like `HAL_TIM_Base_Start(&htim1);` and in the main loop get the pulse count by `pulse_count = TIM1->CNT;` and the number of positions by `positions = pulse_count / 4;` (since there are four pulses per position).
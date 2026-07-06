## ALL daily journals will can be found here.


### 06/07/2036

## TOPIC: researching the componrnts. DATA Sheet reading

so today i am going to research about the componnets and the teach stack i am gonna use. i have the a guide file using claude after discussing are we gonna build, and what are the right and the best value for monay components we should use.
first i will read the full the guide then i will search the about componets and there data sheets.

found the data sheets for the main MCU  STM32F405RGT6, 
<img width="1366" height="682" alt="image" src="https://github.com/user-attachments/assets/512e2687-2a0e-415a-af36-bbb08444ed59" />

neevr used something like this before, it haev 51 gpios that absolutly crazy, lets see how it goes.
<img width="443" height="427" alt="image" src="https://github.com/user-attachments/assets/53779600-2c1e-4f75-a76d-8b32be848c3d" />


lol my system go freez as i open the refrance schemtic website. fahhh

one more thing (for the reviewer) that i always read the almost full data sheets to learn everything about it, this is what i haev done in fallout, just wanted to tell, :)

i was reading the data sheet and get to know that we are usinf the lowest power IC, not the the lowest power but there are what are why better then this. like  STM32F407Ix which haev 140 GPIOs but when i asked my mentor (claude) why not we use the STM32F407Ix he said, 
```
1. Package size — the big one for a drone. STM32F407Ix comes in LQFP176 or UFBGA176 — a huge package (24×24mm or BGA). Your F405RGT6 is LQFP64 (10×10mm). On a weight- and space-constrained 3" toothpick board, that's a massive difference — the 407I package alone could be bigger than your entire current board footprint.
2. BGA is a real assembly problem. If you go with a BGA variant of the 407, you can't hand-solder or even hot-air it reliably — BGA packages have solder balls hidden underneath, invisible during reflow, and typically need X-ray inspection to verify. That's a fab-house assembly service requirement, not a DIY bench build.
3. The extra features are dead weight for a flight controller. F407 adds Ethernet MAC and a camera interface (DCMI) over the F405 — neither is used by Betaflight or any FC firmware. You'd be paying for and routing pins for silicon you'll never touch.
4. Community/reference design mismatch. F405 (and F411, F722, F745) are the actual chips the entire Betaflight hardware ecosystem is built around — that's why OpenESC-style projects and every AIO board reference schematic target these specifically. F407 basically doesn't show up in FC reference designs, so you'd be flying blind without community schematics to check against — the exact thing you told me you wanted to avoid from the start.
5. Cost. F407I parts run more than F405RG for capability you don't need.
Net: F405RGT6 gives you the same core (Cortex-M4, 168MHz, same peripherals that actually matter — SPI, timers, USB) in a smaller, hand-solderable package, with real community backing. F407Ix is the wrong tool here, not a worse version of the right one — it's built for networked embedded systems, not flight controllers.
```
fair point right? this is the reason i prefer reading full data sheet we get to know so many use full things.


i should must keep the temps in my cuz they are really imp. why, cuz i bured few components by not checking the solder tempreture, the SOD light melt instently, lol
<img width="1308" height="332" alt="image" src="https://github.com/user-attachments/assets/cf94e5c9-edc9-4a19-87bb-7ad89c6facb2" />

found the really great info, that i also shoudl keep in mind:
<img width="877" height="560" alt="image" src="https://github.com/user-attachments/assets/d5083598-c3c4-4a48-b856-3f0a5cbbbba6" />


idk if this thing i imp to read, cuz it looks difficult
hell hell hell

<img width="570" height="625" alt="image" src="https://github.com/user-attachments/assets/6f699286-81a3-47fd-b989-8c216b94bfa9" />

maybe i shoudl not miss that imp info, and ask claude to help me understand it.
claude told i dont have to read this completely, just need to find few things and stick with them, this what claude said.
```
Not all of it — and honestly, most of that diagram doesn't apply to you at all.
This block diagram covers the whole family (F405 + F407 together), so it includes stuff like the Ethernet MAC, camera interface, and USB OTG HS — those are F407-only features baked into your F405's chip too but physically don't exist as usable pins in your smaller LQFP64 package. Ignore all of that.
What you actually need to find and understand on this diagram (everything else is noise for this project):

GPIO Port A-I — where your pins physically live
TIM1-TIM14 (the timer blocks) — this is what generates PWM/DShot to your 4 ESCs
SPI1/2/3 — this is your IMU connection
USART1-6 / UART4-5 — this is your ELRS receiver connection
USB OTG FS (not the HS one) — this is your flashing port
ADC1-3 — only relevant if you add the optional current sense later
Power management section (VDD, VDDA, POR/PDR, reset & clock control) — this is what your Phase 1 decoupling caps actually connect to

Don't try to "read" this like a book front to back. Use it like a map — when you're wiring something specific (say, "which SPI do I use for the IMU"), come back to this diagram and trace just that one block. Trying to absorb the whole thing at once is exactly why it looks like hell — it's not written to be read linearly, it's written to be referenced.
You don't need to memorize this. You need to know it exists so when Phase 1 says "assign SPI pins," you know where to look.
```

all i have to focus is on these:
GPIO Port A-I — where your pins physically live
TIM1-TIM14 (the timer blocks) — this is what generates PWM/DShot to your 4 ESCs
SPI1/2/3 — this is your IMU connection
USART1-6 / UART4-5 — this is your ELRS receiver connection
USB OTG FS (not the HS one) — this is your flashing port
ADC1-3 — only relevant if you add the optional current sense later
Power management section (VDD, VDDA, POR/PDR, reset & clock control) — this is what your Phase 1 decoupling caps actually connect to

claude is great subscribe.


umm we have quite good amount of memory

<img width="586" height="283" alt="image" src="https://github.com/user-attachments/assets/2e5b20b7-5582-4209-a7e4-536b853a9de5" />

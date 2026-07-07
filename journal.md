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


now  i have completed the data sheet and now i am confident to start. and i also found a flaw in the look that it dont count time exactly, there is errors in lookout, app i am doing this for morning 11 am and rn its 5pm, and it only counted my time.

<img width="485" height="673" alt="image" src="https://github.com/user-attachments/assets/3880a60f-4af5-4fb2-bd77-8d58bd30242f" />

this is not a small gap this is real things, my hrs are getting wasted, definaltly gonna report this and get my time back, also all other kids might be facing the same problem, so i better report it.


now i am confident, enough to start the schematicts the real thing, now i ahev to find the refrance schematics for  STM32F405RGT6, cuzz i reallly need that thing. after that will go for other thinsg.


i finally found the refrance schematics. it took me soo much browsing.
<img width="838" height="596" alt="image" src="https://github.com/user-attachments/assets/f9bc6014-bf56-4942-a8cc-7c9768ee177f" />


also i wont lose my time again i am getting proofs
here is it.

<img width="1366" height="714" alt="image" src="https://github.com/user-attachments/assets/13d6df0c-89b2-4834-b1b9-3bb2265dc146" />

so now i reead the refrance schematic and now i know what i haev to copy and what is dont have to. i will be starting with STM32F405RGTx then will assign pins, to global labels

building while vibing

<img width="285" height="326" alt="image" src="https://github.com/user-attachments/assets/660d5aea-351b-4607-aeb5-f34fb8a063a7" />


idk why system suks everytime i open kicad.


ohh man KICAD just crashed i hope my data is saved init.


bro wjy i should have saved this is too bad.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/5ba6712b-7b19-4335-bf0d-32b662c17ca3" />


rn i am in lose, i lost the build of schematics, also my system is on the edge it is lagging like hell, it is freezing, 
i was doing macondo to get a decent laptop, but now thats on hold cuzz of arcana , i want to get to the singapore, 

now then i dont have any option left, all i can doo i restart.

I am back at that point where i lost it. yeah i saved it this time, lol


i have fnaally made someting. idk why this took so much time but atlest i fugure it, now i am gonna speed i haev to complete my project before 25 to amke it to singapore.

<img width="359" height="199" alt="image" src="https://github.com/user-attachments/assets/8e552ca7-d99b-4823-a1a3-bbb60b96f9de" />


2 more pins done

<img width="746" height="374" alt="image" src="https://github.com/user-attachments/assets/261d37ec-e20b-46ad-b9d4-915f6c699cd1" />

this is what i haev done soo far. i know this is vey slow, tommorrow i amgoona lock the hard in.

<img width="1167" height="620" alt="image" src="https://github.com/user-attachments/assets/d3bb704a-597c-402b-805a-c8d25b61658b" />

so i have done today work, today i get the things know and get the hand on experience tommorow  u will what i am gonna do, fahhh

and i added one mroe thing. 

<img width="547" height="451" alt="image" src="https://github.com/user-attachments/assets/dedb65ad-6b08-4d5e-858c-1fd4b571a3c5" />

here is how it looks in full pic

<img width="1194" height="614" alt="image" src="https://github.com/user-attachments/assets/701ae41d-d829-4c20-b597-2b2311d46736" />


bye for today.
<p align="center">This text will be perfectly centered.</p>
## THE END

### 07/07/2036

## TOPIC: making schematics


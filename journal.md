## ALL daily journals will can be seen here.


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
<p align="center">THE END</p>


### 07/07/2036

## TOPIC: making schematics

today i will be completeing the my main MCU, and planning to do atlest 5hr today.
lets see how it goes.

i am editing the symbol cuz few pins are not visible and i dont like that, idk why but i want every thing precise and perfect. idk why sob>

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/1666c247-d595-4f07-8ba9-fdc1b0688a93" />

can u see the progress

<img width="943" height="616" alt="image" src="https://github.com/user-attachments/assets/56acf510-a25f-43c4-afa1-5b9d192a3519" />

not gonna stop until i complete the MCU

so i just completd one more item, and i go to referece schematics and i found i am doing wrong i have added the erong values to the C1,C2, i gave them 100pf but these are too much i need only 10pf.
<img width="651" height="504" alt="image" src="https://github.com/user-attachments/assets/e9e26557-b734-41ec-9ed8-c456a88aa3a4" />

also these where missing

<img width="391" height="361" alt="image" src="https://github.com/user-attachments/assets/2c30ed95-49db-4a40-ac9f-d08ac0262647" />


solved 

<img width="666" height="499" alt="image" src="https://github.com/user-attachments/assets/9e9fa71b-4ab0-4e4a-b027-f17c8f8cc2f2" />


added the Indicator light

<img width="683" height="414" alt="image" src="https://github.com/user-attachments/assets/4567650f-5917-48ea-8839-8162b081eee8" />

so i had few confusion on the power VDD33, VBAT, and VDD33A that should i mane them all VDD33, but my mentor said no keep them saprate they have there own works which are sparate, like VDD33 will provids the normal 3.3v but the VDD33A provide by filtering by ferrite bead.

bro idk what to doo the KICAD is get freez again n again.


bruh just found the the biggest blunder i did last night. 
i connected this 

<img width="501" height="267" alt="image" src="https://github.com/user-attachments/assets/06138636-4d30-4f23-9e4c-f5f5882db415" />

with PA pins btu the was gonna get on PC pins.
here

<img width="718" height="246" alt="image" src="https://github.com/user-attachments/assets/02e390b6-eb58-4872-bb26-d7e534202a73" />

now i need to solve this blunder, this si nto hard to solve but this is good i found this early.


now its done:

<img width="1078" height="304" alt="image" src="https://github.com/user-attachments/assets/29906db9-8438-4fab-a2a1-ced6b43ffc24" />


i made this but idk if i did it right or wrong.

<img width="506" height="414" alt="image" src="https://github.com/user-attachments/assets/b938866d-086d-4220-990c-0e8535f16b9b" />

let me ask the grok about it :)

grok said nothing much wrong just placed wrong way.
so i corrected it

<img width="911" height="519" alt="image" src="https://github.com/user-attachments/assets/b7cbf309-bec3-44c8-b248-18b4d0f7e8f9" />


progress can be seen.

now gonna make all these:

<img width="1320" height="335" alt="image" src="https://github.com/user-attachments/assets/114990b8-325b-4fa3-b8be-70a8118e6495" />

SD card one, but i am afraid what this doesnt matcht the schemtics properly, i think my symbol is diff

here is how myn looks, 

<img width="988" height="476" alt="image" src="https://github.com/user-attachments/assets/7e04384d-976d-471e-ac74-ed0f4499cb61" />

theres

<img width="576" height="586" alt="image" src="https://github.com/user-attachments/assets/9d95b9fa-4c28-48b1-8bba-60c0a77ab702" />

just verified it not a big deel myn will work fine too. 


now  the SD CARD is fully done

<img width="903" height="551" alt="image" src="https://github.com/user-attachments/assets/1709c0e0-e929-4f54-98d5-93d1ef57a7b2" />

next is:

<img width="537" height="511" alt="image" src="https://github.com/user-attachments/assets/17a559ef-a7f2-43d3-a6aa-f3da5dfcf589" />


i did the USB C jsut now but idk if this right or wrong.

<img width="865" height="500" alt="image" src="https://github.com/user-attachments/assets/aea2e39f-bf19-4227-8ece-0c9f7b382416" />

i will ask latter in the #hardware help, cuz grok is getting confused. LOL

so the next is

<img width="1007" height="604" alt="image" src="https://github.com/user-attachments/assets/1174f0d0-02b4-4c94-b818-276ccb2493a1" />

bruk i stucked, i need this component 
<img width="262" height="215" alt="image" src="https://github.com/user-attachments/assets/e78e8f62-a6ea-44f1-af15-f076961e9a76" />
 but this is not avalible and after taking with AI and getting pissed nnow i am gonna do it myself

means gonna make it my slef and new sybol for ME6231A33PG

now i have to make the symbol but idk how to make it, i will be my first time
i not able to figure it out, i think i should just watch a youtube tutorial.

broooooooooooooooo
i finally did it.

<img width="519" height="328" alt="image" src="https://github.com/user-attachments/assets/de38942d-df3d-4880-a5d4-6d510e85b232" />

I think i have done something wrong, the pins are not connecting with wires. idk why.

bro finallt done this took me more then 1.5 hrs but atlest at the end i did it,

<img width="846" height="527" alt="image" src="https://github.com/user-attachments/assets/2f0782fc-a043-49a5-8964-bcf1c9ad2e11" />

SO THIS IS END OF SECOND DAY JOURNAL.

bye for today.
<p align="center">THE END</p>


### 06/07/2036

## TOPIC: Doing ICM-20602

figuring out the pinouts.

<img width="1366" height="671" alt="image" src="https://github.com/user-attachments/assets/8f672630-4412-4480-953b-116c4ae538a1" />

nto able to find the data sheets for the ICM-20602.

ohh just find out.

now gonna read it, i will only read few parts, that are imp not all of em, i read all the for STM and regret it total waste of time, just learnt few concepts.

mhmhmhmhm
i  need to must make these thngs to make it stable and auto pilot.
<img width="712" height="317" alt="image" src="https://github.com/user-attachments/assets/181881b7-351f-475c-9f92-e411575b2b8f" />


Ok now i have all enough to get strated with ICM-20602. next is too find the refrance schematics to make sure its will work fine and dont make noise

found this in the KICAD, it is what i want but the pins are missing i think soo, maybe they are hidden.
<img width="706" height="718" alt="image" src="https://github.com/user-attachments/assets/c392f84c-51b1-4ba2-b279-3aff15d7f291" />
<img width="726" height="501" alt="image" src="https://github.com/user-attachments/assets/e3cd7fea-48ce-43af-a582-b9c896af98b1" />


the KICAD symbols of the ICM-20602 was a bit wrong in the both KICAD and the refrance schematics but no worries i have correcte it, so myy ancestors wont have to struggle, LOL. i mean i have redisign the whole symbol to match same as the refrance one.


bro i messed up the pins are not connectinf, i think i did set it right way


finally bro did it, this is hell i dont have option else then this except to use standard symbol, and i cant use it cuzz i want to fully match the schemtics and this will help me figure out things latter.

now all pins connect with wires

 <img width="484" height="316" alt="image" src="https://github.com/user-attachments/assets/ae5a3dd2-64ca-4ecc-a9bc-7f5876151e75" />


i am finally done with ICM-20602 this shit, actully this is not shit that refrance sch was, idk who tf made that there was soo many mistakes. i had to solve them that took soo long. 

but altelst at the end i did it.

<img width="796" height="456" alt="image" src="https://github.com/user-attachments/assets/453dfa18-35bb-41c9-ad18-0e1e132a0d1f" />


bro next goona take even more time.

this goona be complete setup of 2-3 components that will work with moter so every mototr will have its own this setup, this what my mentors guide says:

<img width="554" height="614" alt="image" src="https://github.com/user-attachments/assets/4ab11fd5-f1af-4e49-a313-faa766dea184" />


bruh next Phase looks really hard
<img width="833" height="449" alt="image" src="https://github.com/user-attachments/assets/a2266101-6524-403b-8621-9833ecb8c86f" />


my mentor give datasheet that is in chinese how the hell i am goona translate it> metors sucks sometimes

found the right one in english:
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/1f7b30bb-4f2d-40f5-bb98-192772ed045c" />

<p align="center">THE END</p>


### 09/07/2036

## TOPIC:pahse 3 three hardest part


so last day its was  very bad day, i only did 2.5 hrs but i need to do the 10hrs per day, but anyway today we are goona do the phase 3:

<img width="656" height="634" alt="image" src="https://github.com/user-attachments/assets/bfcc7d80-ab05-45e6-92ab-0c544f4e6dc5" />

why the it is too hard to find the perfect symbol, bro this sucks, the symbol i found is diff from the schemtics one

bro i found but i cant download it idk why it is on JLCPCB for eaasyday but it is not downloading and i also cant  fidn anywhere else.

<img width="281" height="276" alt="image" src="https://github.com/user-attachments/assets/513dcb50-d362-45ac-9663-d6f9f774eef7" />

maybe i should make my own by replicaating it.
 so yes i am goinfto make my own. wish me GL


SO FAR SO GOOD 
<img width="388" height="375" alt="image" src="https://github.com/user-attachments/assets/baab751e-8405-42f2-a4f3-f8c36ab9f4f1" />


FINALLY DID IT MAN
<img width="650" height="570" alt="image" src="https://github.com/user-attachments/assets/375990d1-d500-492f-9018-1a7b090f9f66" />

i ma feeling pround now, cuz when i go span for this symbol they siad they will make me one but for 29$, and i made it myslef, ayayayyaya


but the most dificult thing still remins, the FOOTPRINT  and i never mmade it before. this gonna eb hard


it is too confusing to make the the footpritn i dk what to do maybe i will watch the toutorial:

bro its tooo hard. fahhhhhhhhhhhhhhhhhhhhhhhhhhh

i think i am doing something, not sure if this is right or wrong but still doing it.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/fdad8dd2-ee3d-4ded-8bc6-4b53bc32a423" />


bro why is this tooo hard, i ahev to take care of every mm and after more then 30 min i only did right side and i am not even sure if it is right or wrong

<img width="592" height="526" alt="image" src="https://github.com/user-attachments/assets/4f1a526c-a900-4bc9-b37b-ff2298e3b47d" />


bro finally this is perfect now

<img width="579" height="528" alt="image" src="https://github.com/user-attachments/assets/12d310c6-c6b3-4202-b68f-41050e667b18" />

finally completed
just numbering left for padds

<img width="357" height="313" alt="image" src="https://github.com/user-attachments/assets/e5fcd680-f140-4295-9b03-daf3a8268cfd" />

completed

<img width="662" height="471" alt="image" src="https://github.com/user-attachments/assets/0734dc01-223f-440a-807f-2090ba943992" />


I DID SOME SCH WORK AND 1 ITEM IS DONE, THIS IS THE SYMBOL I GRINDED FOR:

<img width="757" height="461" alt="image" src="https://github.com/user-attachments/assets/28c35b0e-3bcd-447f-ae9c-4b8d6a5c0385" />


i wonder why the hack the kicad symbols and the refrace schemtics symbols are no the same shpae, it tok t much tme to verify that pins are correct the the symbol is correct or not.

<img width="1261" height="585" alt="image" src="https://github.com/user-attachments/assets/ff4358cb-102e-4bd8-99e2-84558c31e4c6" />


went to the break for 2hrs,now i am back fully charged, not goona sleep until complete this phase.


i really needa new laptop, form morning the KICAd have crashed more then 4 times, this is bad, it is slowing me down.


I DID some work, it was so confusing referance schematics that it took me sooo much time and still idk so many things init, and this is the best datasheet i found, there is one item idk what is it, and i havent added it yet, first i will confirm it then i will add it.

<img width="262" height="193" alt="image" src="https://github.com/user-attachments/assets/efb3998d-f0dc-4054-a5c4-c2723b917672" />

this is where i am rn, sub

<img width="395" height="318" alt="image" src="https://github.com/user-attachments/assets/da07ea9d-d1b8-41fa-91e9-9d5508d3921d" />


fahhhhh, idk waana drink coffee anymore, sooo

<img width="660" height="679" alt="image" src="https://github.com/user-attachments/assets/a7648d57-ca77-403b-a92d-954c413096b9" />


i have completed the 90& of the 1st item of this phase, i still have confusion on the few lebals and components. who made this refrance schemtics must me crazy.

this is how myn looks rn:

<img width="1366" height="765" alt="image" src="https://github.com/user-attachments/assets/2ae71e99-f67c-4c9d-a7fc-bc7d926b7847" />

this thing have serious effort of me, i made sybols and footprints, it must be right now.


i have done areally good, job, what i made in schematis is correct and i have verified it, the only thing i am missing now is the C and R values idk what values ot give them, and the refrace schemaitcs dont have them either.

finally it is almost done, one of the mot difficult things will be ending soon, and u cant imagine, how much my head hurts, cuz its 2am at night, fahhhh

its  now fully done, there no item in PHASe 2 thar is icomplete, everything is done. 

<img width="1010" height="536" alt="image" src="https://github.com/user-attachments/assets/b7e4fa04-dd5c-4bf3-8098-845e8c4ee692" />

<img width="1010" height="536" alt="image" src="https://github.com/user-attachments/assets/c8b05c35-08e8-48ca-9c10-54a938d4ff1c" />

THANK GOD THIS IS DONE OR I WILL BE DEAD FRRR, 

i cant even explain, my condition rn, my eyes are full red rn and my head and back is paining hard, 

BUT I THINK IT IS WORTH IT:

<img width="1366" height="678" alt="image" src="https://github.com/user-attachments/assets/8fed84cd-19c1-4d26-bdd0-a0e4add16d7a" />


<p align="center">THE END</p>


### 10/07/2036

## TOPIC: phase 4


so last day i completed the phase 3 and now i am gonna move to the phase 4.

organized the schematics a lil bit.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/f0cf24a6-f6ef-4e4a-842b-1c5e679c49f4" />


pahse 4 is a bit confusing, altough i have done this thing befre but it is locked in my subconscious memory, lol. 

<img width="915" height="594" alt="image" src="https://github.com/user-attachments/assets/3215bfb7-1bb4-4485-91ed-a4acc57a1470" />

ohh dman man htere are websites where if need any refrance schematcs we have to upload 4-5 docs to get that, alsolute shit


my lap is getting freez again and again. this is soo frustrating, 


i have almost finshed the phase 4, only batter connection left, its wasnt that hard how it looks it was just confusing.

<img width="1083" height="573" alt="image" src="https://github.com/user-attachments/assets/3da667d3-c72e-491d-b1cd-5af57c986e5c" />

arranged them so it wont looks mess

<img width="761" height="549" alt="image" src="https://github.com/user-attachments/assets/7d1bd16e-6bdd-4f6c-9982-48dc65726fb4" />


so i have completed the phase 4 now the only phase 5 left then ERC and then PCB and DRC

<img width="785" height="616" alt="image" src="https://github.com/user-attachments/assets/dffd0c7e-e166-4a03-b570-8e26938de2f0" />

so now i cant find the, MAX7456 / AT7456 KICAD symbols and its refrance schematics

, so i ahev found the symbol but it in the someones repo so i need to clone the repo or download that file. SOB

got it

<img width="640" height="615" alt="image" src="https://github.com/user-attachments/assets/563f571b-6495-497a-801e-4b629839a80d" />

bro why tf is this shit too expensive, is it made of gold, damn this is shit i will stick with cheaper verionAT7456E

<img width="859" height="455" alt="image" src="https://github.com/user-attachments/assets/a753925d-fc0d-449a-8475-90ce2604f15f" />

yoo man i was stressing for nothing, after some research i get to now that both MAX7456EUI+ and AT7456E are the same just clone to each other, so they have same KICAD symbol, and footprint and the the refrance schemaatics is also same for both of em.

OSD Completed:

<img width="700" height="469" alt="image" src="https://github.com/user-attachments/assets/b05d432f-1d35-4197-9ea4-cbc7e8b70a6a" />

also i have coloured the conntion of the ccompoents to the STm so if anyone wants to recreate this he will eb able to do it easily.

<img width="395" height="500" alt="image" src="https://github.com/user-attachments/assets/0b61194b-ca7b-4955-a079-8726cd34ca74" />
<img width="1015" height="570" alt="image" src="https://github.com/user-attachments/assets/10742fb3-9c31-4d4f-a988-f688fab3f27a" />
<img width="514" height="418" alt="image" src="https://github.com/user-attachments/assets/cc3f10ca-f975-4c4f-bea3-43b590adcf90" />


looks even better now.

<img width="459" height="502" alt="image" src="https://github.com/user-attachments/assets/4a1af1a9-ac0a-4da9-a430-cfab0eb742a0" />

there where some wrong connections in the OSD i have corrected them , and also did the USB-C 16pin

<img width="670" height="616" alt="image" src="https://github.com/user-attachments/assets/ebd46bac-e236-4989-809e-6c9ad4de27cd" />


<img width="1023" height="582" alt="image" src="https://github.com/user-attachments/assets/43145675-be00-436c-ab81-c6ae4ebd5cc5" />


i added the USB C so it will be easy to flash the firmwre but now i get to know that STM32F405RGTx have specific pins for USB we canot reman as wee need and the that pins are alredy in the use of ESC pins. 

i think i should remove the USB C and stay on SW headers. 


so i was doing the BMP280 and i get confused on the pins that will be connected to the our STM32F405RGTx so i asked it to ai, PLZZ dont cut too much time, thanks. 

idk why i just pulled up with the help of AI, but i hope this is correct.**HI**

<img width="1085" height="553" alt="image" src="https://github.com/user-attachments/assets/49d433ea-6311-468f-b9d3-e19cc5474622" />


it was wrong, 

<img width="735" height="506" alt="image" src="https://github.com/user-attachments/assets/2a6fcc2c-bb47-4159-9e15-bbd06b55cca7" />

also there is no fast pins left on our MCU so i will be connecting its pins will rendom available pins.


Soo colorful

<img width="807" height="589" alt="image" src="https://github.com/user-attachments/assets/cccb04f0-ba21-4f7d-a0fc-3f401059609c" />


so the schemmatics is now done, i think this is it for schematics, we have everything to that will make drone fly.

its time for ERc lets see what hellish errors we got.


not much but not less eithr.

<img width="676" height="663" alt="image" src="https://github.com/user-attachments/assets/2d3445d4-ff43-4fe4-b5c0-93a9bd3805c8" />


brouh i i have soo many messes in the schematics, and rn i cant find the refrance schematics.

damn man i speant 30min searing for pin connection but at the the end it was GND. FAHHHHHHHHHHHHH

i am using AI to solve a error plzz, consider this a nothing. 

ohh man playop is hanginn 


the kind of shit i am listening to keep my self swake.

<img width="1363" height="710" alt="image" src="https://github.com/user-attachments/assets/3855ad0d-e14f-40fa-9773-1f1062e74701" />

the error where not that hard just needed to chnage the pin type form input to output and passive, now only 5 error left, i think i should solve them before i sleep.

yes i shoould.

<img width="662" height="608" alt="image" src="https://github.com/user-attachments/assets/77112568-7246-4d21-b6e6-3e4c540a3fa1" />

now only one error left

damn man stuck on the last error 

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/08de6f52-632a-4ba7-b679-4e662d3b48e2" />

SO this is it for today.

bye

bye for today.
<p align="center">THE END</p>


### 11/07/2036

## TOPIC: finshing the schemtics and solveing all error and moving to MCB.

so last day i completd the schematic, and was solveing the error but 1 error remains, and its a bit confusing.


now bro everything is done in schematics all ERC error are gone also there where some hidden error is the warining i have solved them too, so next i will be going to assign the footpints to the all components.

bro i messed up on battery connections, i used JST that is for low currents but i didnt know that for drones we need XT60PW-M to handel that much current.

also why tf battery are soo halla expensive


corrected the Battery conection.

<img width="481" height="385" alt="image" src="https://github.com/user-attachments/assets/05d6e718-63e4-4c67-b159-3d18c5c1bfc4" />


i am, getting so frustrated rn, what the hell is with my laptop the symbol i made and its footprint was lost then i had to find, also soo many compoenents are confusing its getting to hard step by step, i am really losing


now i ahev to make a acoount to get open source footprint. seriously


so i ahev added 3model to the footprints not to all of them but few. i stoed cuz i found few mistakes that i have to solve before i move to anything else. also i havent added the MOSSFET footprints yet cuzz i didnt found  any, this ill be bad.

<img width="1074" height="606" alt="image" src="https://github.com/user-attachments/assets/ba402809-895a-4421-b631-ec3bba5ad4b2" />


the only symbols left now is this

<img width="665" height="463" alt="image" src="https://github.com/user-attachments/assets/363c5b85-bade-4990-a494-12ec311b3203" />

also i maybe have to redesign its symbol cuzz according tp google ur symbol must be same as footpint ur chosing but our are diff cuzz i didnt found the correct symbols

my brain is not brianing, cuz of these shitty MOSSFET, this shit is widely being used in drone but it dont have exact symbol and footprints, total shit.


i am opening that github guy schematics to see what symbol and footprints he is using .

bro what the hack that repo guy did to this, looks more like a creepy insect then PCB

<img width="814" height="650" alt="image" src="https://github.com/user-attachments/assets/bebffb17-8e4c-4618-ba0a-af9c269001bb" />

<img width="1013" height="609" alt="image" src="https://github.com/user-attachments/assets/16e794d4-9e03-4275-b57a-91caa9d26afa" />

bro this schemtics dont haev the things that i need, idk what is that but that is not what i am looking for, total waste of time.

oh bro hes verion is right an we i am very close i just need to extract the footprint from here, all other things are correct on my end, i was stressing fot nothing;
he is using same lebals as i 

<img width="1213" height="354" alt="image" src="https://github.com/user-attachments/assets/51403df4-ff70-4e5e-ac80-0f155f4c64db" />

OHH man finally got the footprint; Diodes_PowerDI3333-8 in package son

this is not a normal man look how badass he is , soo professional

i wonder how much time took hin to do this

<img width="900" height="563" alt="image" src="https://github.com/user-attachments/assets/aecf3c58-99f6-4741-a602-e501a54c01e3" />

u what, my laptop is too weird if any app stops responding i trys to restart the app by task amnager but task manager also stops responding, heelish hell

just completed all the footprints now the next part is my favrouit THE ROUTING part, i love this.

broooooo

this does not look good>

<img width="697" height="521" alt="image" src="https://github.com/user-attachments/assets/e68cfd73-b150-494e-b398-75e9ee4f6822" />

idk why but it dont, even thothat repo man had the same symbols but i think i missed something there..

now idk what design i should take for PCB like a small square or a rectangular, i think rectangular will be better, but still i will reserch on it.

how much i searched the square one is better, but will still add the small req in it, soo it will beeasy to route.
 i made an rough one , to see if it fits ir not and it is fitting perfectly in 50X50


i have to make new design where all components will setell the best way.

<img width="480" height="461" alt="image" src="https://github.com/user-attachments/assets/649658fd-5c96-40e2-a74b-617c08d87265" />


i made this but idk ehy it is not working i rechecked it but still not working


now i have very good design but it is not workking, idk why         SOB 

yayayyayayayayay
finally

<img width="787" height="538" alt="image" src="https://github.com/user-attachments/assets/4918ae96-b4f7-451b-89c5-6783eeaa1a0b" />

i am placinf components very slowly and precisely, cud i dont wan tany mess i will take time but make it best

first phase done

<img width="863" height="525" alt="image" src="https://github.com/user-attachments/assets/c6fe86c7-2661-4e57-bb40-80a6e6b8d2eb" />

<img width="788" height="509" alt="image" src="https://github.com/user-attachments/assets/54244590-acd4-4f8b-b5eb-93df503b8544" />

<img width="1246" height="707" alt="image" src="https://github.com/user-attachments/assets/6da37170-b673-4122-a9d7-dd1fa2c17f92" />

hey i had a SD in the shematics i think i should delete it cuz i dont find any crusial use case


bro i deleted the SD card got this in return gify, tf

<img width="636" height="50" alt="image" src="https://github.com/user-attachments/assets/cee7e567-da5e-4f33-8304-0876e7c2e3fa" />

can u see the amount of work done, and still going ggggggggsssssssssssssssss

<img width="547" height="402" alt="image" src="https://github.com/user-attachments/assets/de40d29f-3442-41ae-9365-05c9e8abacd7" />


bye for today.
<p align="center">THE END</p>

### 012/07/2036

## TOPIC: trace routing

last day i finalized the schematics and today i am will be routhing.

i am arranging the set of components as accurate as possible to keep drone stabel and so barometer can work perfectly. 

so i will be placcing complete 4 esc channels on back and other will be on from 

for the channels i have to bee soo precise so it will be easy to route them, i have done 1 channel now i will place other on it anf then just flip then this i will have all 5 channels in same accurate structure.

<img width="456" height="418" alt="image" src="https://github.com/user-attachments/assets/cc631cd7-b8f7-489e-8245-8d1484d58010" />

exactly as we wanted ayyayayayay

<img width="956" height="556" alt="image" src="https://github.com/user-attachments/assets/cefa9e45-0938-4fec-8c1c-2cdff929f6bb" />

<img width="947" height="480" alt="image" src="https://github.com/user-attachments/assets/e204133e-8a9c-4417-9578-8670a21e58d1" />

i was think of replacing the JST with the test pads if these can flash as JST. cuzz JST is taking so much space.

gonna add the test points footprints, this these wont take much space and they will be waightless. 
WINWIN
so i am going to use the test pads here how they looks

<img width="578" height="276" alt="image" src="https://github.com/user-attachments/assets/0cf88b65-475a-44fd-90bd-1dcf9c4ad26e" />

Much better then before

<img width="392" height="377" alt="image" src="https://github.com/user-attachments/assets/2aa9a04f-29e4-47b1-8748-680979e71e71" />
<img width="567" height="370" alt="image" src="https://github.com/user-attachments/assets/f8ca0490-83d3-4934-a30e-9f61aae5523b" />

goiing soo good soo far yayayayyaya

<img width="1064" height="608" alt="image" src="https://github.com/user-attachments/assets/6931779c-7270-48d7-b245-8aef94451f17" />
<img width="947" height="568" alt="image" src="https://github.com/user-attachments/assets/8dbef08c-bc4e-49dc-ae21-2f6840342f75" />

the method i am using for compoenents takes but work soo well, almost 100% accurate

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/e2eb320d-5cdf-4b30-8d16-e460fe8c47fe" />


finally did it:

<img width="712" height="541" alt="image" src="https://github.com/user-attachments/assets/b7e286b8-1947-4b50-a30b-4f587c424cd4" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/0ecb6707-420e-434f-87f2-45373eb9b389" />

bro i am still confused about our mossets, idk if they ar ecorrect or not. i have a bad feeling so i am checking it one last time.


ok so my biggest stress is gone, i had very confusion on the MOSSETS but now it clered, but no i have to change few things in the schematics and PCB both, then routing,
this project will be hardest thing i ever build, 


finally the stress hthing is now gone. yyayyayaya

<img width="661" height="580" alt="image" src="https://github.com/user-attachments/assets/e9ec37cb-057e-4cfa-be16-2bfbc9c02ba1" />


bro i locked the components now i dont know how to unlock them.

<img width="682" height="560" alt="image" src="https://github.com/user-attachments/assets/024431b9-efe9-4426-9581-d804e14087a5" />


BRO KICAD crashed and my component placment rest, fahhhhhhhhhh

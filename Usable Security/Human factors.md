# Human factors 2a
![[Pasted image 20230712103106.png]]

## Aims of the lecture:
1. Understand the elements that define usability  
2. Criteria for effective design  
3. Know human capabilities and limitations, and how they shape  
interaction with security



## 1. Understand the elements that define usability  
The way to make security that works is to make security that  
works for people” (NCSC)  
• How? → Human Factors principles:  
“fit the task to the human” (through design) 90%  
• Only 10%:  
“fit the human to the task” through security awareness and  
education
## 2. Criteria for effective design

1. Effectiveness: the accuracy and completeness with which specified users can achieve specified goals in particular environments.
	-> can users complete the task?
	bad examples: to many user prompts when creating a strong password
1. Efficiency: the resources expended in relation to the accuracy and completeness of goals achieved 
	-> which/how many resources does it take to complete the task? 
	time and effort trade-off?
1. Satisfaction: the comfort and acceptability of the work system to its users and other people affected by its use
	-> how do users feel after completing the task?
	- comfort: do they feel tired? annoyed? confident of having done the right thing?
	- acceptability: Do they want to do it? Do they feel the time and effort is worth it?
 bad examples: disruptive security measures: sending hoax with bonus promise to test employees -> non acceptability


How we “fit the task to the human”?
1. The capabilities and limitations of the target users
2. The goals those users have, and the tasks they carry out to
achieve them
3. The physical and social context of use


## 3. Know human capabilities and limitations, and how they shape  interaction with security
Human capabilities and limitations  
• Capabilities: things people can do (well)  
• Limitations: tasks they can’t do (well)  
− Physical:  
operating equipment, e.g., pointing and pushing buttons  
human body  
Examples:
− size, e.g., height and finger size  
− motor skills, especially older population  
• wheelchair users  
• very tall or short user  
• Blind or vision-impaired  
• colour-blind or colour-weak users

Bsp.:
- zu kleine Tasten auf Gerät, Gerät hängt zu hoch für Rollstuhlfahrer(z.B. Bank),
	Bilder Authentisierung im Internet unmöglich für blinde Personen
	
− Perception:  
detecting and processing signals  
(visual, auditory, haptic – plus smell and taste)  
Examples:
• Humans are good at detecting, recognizing, and matching visual  
patterns (even when they don’t exist)  
• Signal detection: not good a detecting  
− Rare events (brain stops processing)  
− Small incremental changes (frog boiler problem)

-Bsp.:  
- offenes und geschlossenes Schlosssymbol bei sicheren TLS Verbindung, mehrere Kameraansichten gleichzeitig bei Kameraüberwachung, Scan-Systeme an Flughäfen, oft falsches Monitoring

− Cognitive:  
attention, memory, knowledge (mental models),  
decision-making, language

• Attention: people have only one focus of attention – multi-  
tasking comes at cost (time, error)  
• Memory: human memory is selective, constantly evolving  
• Knowledge: structured around “mental models”  
• Decision-making: subject to biases


Bsp.: 
- Photo-Tan gerade(einfach) vs. ungerade Anzahl an characters, homogene character einfacher als heterogene
- aided recall (recognition) is easier than unaided recall(remembering)
	--> graphical recognition is easier than remembering passwords
- interference effect: similar items compete on retrieval,
strongest comes out first
- memory biases (people pick easy passwords,{image credentials} prefer strong colours and shapes, {image credentials} tend to choose passfaces of their own ethnic, {image credentials} people prefer features that stand out),
  people use locations on keyboard for 4-digit PIN remembering, order of elements depends on language left-to-right or right-to-left, finger swipe passwords don't have a lot of entropy
  
### Main aspects of human factors 2a
1. always fit security tasks to the intended users
2. that means: research and designing for their capabilities and limitations
3. blaming people, because of limitations is stupid
4. unusable security violates accessibility guidelines and can lead to exclusion


# Human factors 2b

## Aims of the lecture:
1. Understand how goals and tasks drive user interaction  
2. Know the distinction between secondary and primary tasks,  
	and how to apply this to the design of security tasks.  
3. Know what workload is, how you measure it.  
4. Know environmental (physical and social) factors and how  
	they impact security solutions.


circumvent= etwas. umgehen



## Goals and tasks
- human activity is essentially goal-driven
- humans carry out a set of tasks to achieve a goal
- tasks can be decomposed into sub-tasks, sub-sub tasks etc, until we reach a single (atomic) action


### frequent vs. infrequent
depending on the frequency of the task, the development of the task differentiates 
- Frequent tasks (several times a week, or more):
	− Most likely to be automatic – becomes a routine or habit
	− Design: optimise for speed execution, low physical effort
-  Infrequent tasks (once a week, or less):
	− User needs to consciously recall and execute each step
	− Design: guide user step-by-step, minimise recall
	− Execution time less important

-> task performance is measured by:
1) effectiveness: task completion, quality of result, errors
2) efficiency: time, effort(workload)
3) user satisfaction: perceived quality, effort, confidence
-> as well since security is a secondary task, we need to consider requirement of/impact on primary task


## 2. Know the distinction between secondary and primary tasks, and how to apply this to the design of security tasks.  
Primary vs. secondary task  
• Humans focus on their primary tasks  
	− What they are trained for, where they have core expertise  
	− What they are rewarded for  
• Secondary tasks can be seen as:  
	− Obstacles or distractions  
	-> creates friction until compliance threshold is reached and users start to circumvent + coping strategies
	− Cost vs. benefit to individual vs. organisation  
• On some occasions, security can become a primary task

-> interrupting primary tasks always has a high cost, keep that in mind when placing security tasks(at  the beginning or end)


## 3. Measuring workload  
Measuring workload refers to the physical, perceptual  and cognitive(mental) (limitations) as well
- humans prefer extra physical over extra mental workload
• Analytically: KLM-GOMS  
− break down user tasks into simple actions  
− estimate / predict time task will take  
• Empirically: NASA-TLX (Task Load Index)  
− ask users to complete task  
− rate effort

## 4. Know environmental (physical and social) factors and how  they impact security solutions.
physical and social environment can impact human-system interaction -> always reflect the context of usage
Physical context
1. Lighting – esp. impact on screens and cameras  
2. Noise  
3. Ambient temperature  
4. Pollution

same aspects impact probability to start an attack regarding the CCO
![[Attacks and Attackers 2#Wider environment]]

Social Context  
• Human activity is inherently social – governed by values and behavioural norms  
• Individual vs. organisational values: value conflicts induce  humans to circumvent secondary tasks such as security and safety  
• Social norms (e.g., politeness, helpfulness, trust) drive human behaviour: if security policies match norms, people are unlikely to comply

### Summary
We have many factors to consider when we try to construct a
security solution that “fits”:
▪ in addition to user capabilities and limitations
▪ user goals, and the tasks they carry out to achieve them
▪ the physical and social context in which that interaction
takes place



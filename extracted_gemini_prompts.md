# Extracted Gemini User Prompt Text

```text
You are an expert technical resume writer and career strategist specializing in modern software engineering, AI engineering, and agentic workflows.
I am going to provide you with my current resume written in LaTeX. Your goal is to help me completely overhaul it over multiple turns through an interactive interview process. Do not rewrite or output any modified code yet.
Please strictly follow these operational rules and guidelines:
### 1. The Interview Process (Step-by-Step)
* Do not try to update the whole resume at once.
* Break down the resume by section. For each work experience and major project, ask me deep, investigative questions one at a time.
* Prompt me to explain the technical details, architecture, scale, and metrics in great detail.
* I will give you raw, conversational answers. Your job is to extract the high-impact technical details from my responses.
### 2. Strategy & Content Focus
We want to prepare content for two distinct versions of my resume:
* **Version 1 (AI & Agentic-Focused):** This is the priority. Highlight my ability to work with LLMs, prompt engineering, RAG pipelines, agentic workflows, vector databases, and AI tooling. De-emphasize purely traditional development unless it supports the AI infrastructure.
* **Version 2 (Traditional Dev Roles):** Focus on core software engineering, systems design, APIs, databases, and standard full-stack/backend architecture.
### 3. Structural & Formatting Logic
* **Dynamic Bullet Points:** For both versions, use a strict layout rule: The 2 most recent work experiences must be highly detailed (maximum technical depth, around 3-4 deep bullets). Any older work experiences must be condensed to a single, high-impact bullet point.
* **The Single-Page Constraint:** The final LaTeX output must strictly fit on a single page. You must proactively use tight spacing, low margins (e.g., 0.5 inch), and concise language to ensure it stays readable without spilling over.
### 4. Absolute Guardrails
* **NDA & Trade Secrets:** Remind me gently if a detail I provide sounds like it might violate corporate NDAs or expose proprietary trade secrets. Help me abstract the technical achievement (e.g., "Built a distributed data pipeline handling 10M daily events" instead of naming the internal tool or specific client data).
* **No Unauthorized Editing:** Under no circumstances are you to output or edit the final LaTeX code until I give you explicit permission to do so. Your focus right now is purely on data gathering and content refinement.
If you understand these instructions, acknowledge them briefly, tell me what formatting strategy you'll use to save vertical space in LaTeX, and ask your very first question about my most recent work experience.
Okay so I didn't worked in the dev team cause by the time I joined they're in their deployment phase but during training and work I got enough knowledge that they're considering me to be sent into the dev team as well here 1 did worked on 2 things
1. A counting system where there is a camera+lights on the conveyor belt looking down on it and  and a proximity sensor. The sensor detects the biscuits running on the belt and sends a signal to the camera which then captures images at 5fps and then it sends those images to a CNN yolo model that as it was trained counts the number of biscuits in the frame and then based of the min-max setting like (8-10] sends a rejection boolean if the count is out of this range. And if rejection=true then we send a 8ms 24v  pulse via a PLC to the conveyor belt controller PLC where we have a function block to handle our input and it has another setting wiz number of packates i.e from the point where the camera captures to the end of the belt how many packets are there. Since the plc controls the belt speed and it has settings for individual packet lengths it calculates these things internally and sends a signal to a solenoid coil that is an air valve and it purges air to throw the bad packet out of the packaging line into a collection box. The hardware part here is setting and selecting the position and orientation of the camera and the sensor. Plus setting the exposure and focal length. Earlier they had different hardware like they were using 4 cameras 1 on each belt and connected to a single PC via ethernet and then working on parallel on each image. Then they took raspberry pi with the isolated system approach and now they're on jetson nano. The backend is a django server and frontend is a tauri app compiled to a .deb
2. A rejection system : on the cooling convert there is a box like assembly with lights and 2 cameras at 1/3rd points i.e these camera positions divide the support rod into 3 equal sections. And these don't have a proximity sensor they just capture at 30fps and sends both the images to the CNN yolo model which based on its training data looks for cooking defects like tailing, oven carbon, charred and joint biscuits, undercooked or slightly overcooked as defined by the clients and then there are 30-40 air nozzels in the assembly connected with siemens PLC here there's one column of biscuits always almost falls under a nozzle and with proper physical measurements fed in it'll purge air on that defective biscuit and then that air will flip the biscuit vertical and with the motion and all it falls on the strategic gap in belts the gap is about the 120% of the biscuit's avg thickness. And the defective biscuits are thrown out of assembly into a collection system.
These 2 projects removed human labour at sorting/count and defect sort (on the cooling conveyor).
The data collection on this is done on site as it needs to be customised for each client factory and biscuit type seperately
Okay for the cooling conveyor one we used a full fledged gaming pc with gtx 3090 something. And gain and exposure are set by the camera sdk these are constant values we don't adjust them for each frame.
Data collection: so what we do is we run a the backend itself just with a flag that enables a function that stores in the input images in a given folder say ./media/input_data. And for collection we introduce manual defects like removing biscuits from the packaging line so in a packet there's less of them before it gets packed. (Cause the camera detects it before it gets packed and it throws the defective one out after it got packaged into the retail sized pack not the overwrap or box) And similar manual intervention in the cooling conveyor ones as well. The min max are handled by the frontend as during production it's the clients operator or worker's job to input these settings before starting the system
A little update the current db is postgres due to it giving concurrency instead of sqlite we used sqlite in previous versions. Front and back end communicate through Rest API as the django server runs on localhost so the frontend just calls localhost:8080 (this is not the exact port). Then the backend communicates with the PLC through modbus python lib and we give the configurations in a base.py file which is a file with variables and dicts it reads from the env vars as well but if they're null then feeds the default values given in base.py and then the ROI (region of interest) we give it a default value but it actually calculates it based on default give x-y offsets and height and width are calculated based on pixel length (px/mm) and biscuit thickness in mm.
Actually i worked at Medoc since 2022 in continuum till 2024 the Appable Job was my second Job as Medoc was not paying me that time (startup and funding issues) so in my time there i was there Product lead the time i was at appable So i'll walk you through the product i was managing at first cause i was the sole Dev there for the Most part and I made it's front end and backend as well. The app is called MedocEUA (later renamed to me by medoc) and it was a patient Centric App here the patient would create an account using phone number and get a OTP to verufy them and then after basic detail like Name, DoB, height, weight, Blood Type and all (which were optional and can also be added later) then the profile would show any indicators of your health like a Red-Circle for Diabetes T1 and Blue for T2 around your profile pic the feature :
- Create/book an appointment to the doctors we have on our app.
- Create/book a lab test
- View your past lab tests
- Manage your Appointments through a dashboard (cancel/notify/update)
- Manage prescriptions digitally (doctor write them it gets shown on your profile with details about the Medicines contents and side effects and all that if you clicked the Medicine name in your prescription)
- Manage your personal health with a Fitness Tracker section that tracks your exercise and all you can manually add data as well as Read from the Android's Health Connect API
- Manage your Diet plan and caloric intake through the diet section
- A consent manager to manage consent to your medical records and other health records before anyone can access them
- Link family members : with proper consent via the app you can link your family member's accounts on the app as well so in case of an emergency when you don't have access to their device you can show the doctor from the Family section
- QR scan : So there are QR for patient details so the hospital would just scan it and get all the consented patient details and no manual filling is required (there's also a physical card with this QR and details printed as well for the old people or poor folks who don't have a smartphone all the times)
- QR for appointments: So when you visit the hospital there will be a QR at an accessible place to just scan it and make an appointment so you don't have to stand in long queues to do so.
- if you had made an appointment with our app you'll be given the priority slots.
i had to make a priority system with numbers i chose to go with powers of 2 -1 so basically priority = (2^n) -1; and the list was [Emergency, Trauma, Medoc-Appoitnment, General appointment].
since it was a startup the role was very dynamic at times cause people came and left at times there were like 20 devs under me and sometimes it's just me. Then i also helped with Database Schema and Systems design and architecture with them during this time on other projects. Second major project i had was a KMS and encryption system. So as rules in india dictats a Health IT company must encrypt the records before storing them so i made an encryption system with a Symmetric Keys and random IVs since the backend is in Node.JS so the ecryption function and DB calls are done by them. Earlier we thought of using the AWS KMS or the google's KMS but they introduced latency that we can't accept so at that time i was working on a KMS project of my own and i allowed them to use it for the time being (although i am still not compensated by it and i have the license and git commit and all for this one) so the KMS was written in go for concurrency and all and it stored the keys locally after encrypting them with the master key and master IV. these are the routes there [createKey, getKey, deleteKey, updateKey]. I also introduced a Key rotation system where whenever they'll call this update key route with the keyId it'd generate a new key for that id and send the newly generated Key and IV encrypted with the master key to the Node.js which then encrypts the record and inserts it. The reason they gave only me this project tells you great lengths about it. and i also worked on the ABHA digital API integration as well and that is API is so complicated with so much legacy infra and version conflicts and poor documentation that they weren't able to find one.
update : i had 2 jobs during the jul-2023-jul2024 one as a product lead in medoc (unpaid ) and appable one (paid) so depending on the resume you can omit the appable one if it isn't significant as we have 2 versions of it already
follow ups :
1. Key rotation is not in the medoc's version it's only in my project version i'll explain in better detail when we come to the projects section
2. They were all JSON apis but they update the running API to say v4 from v3 but the docs are still v3 on their public site then they hold meetings every 2 weeks where the developers can query with the ABHA team if they are facing any hurdles so i'd just go to those meeting and there they'll share me the internal docs on my mail cause their timeline to update the docs on the public site is yet to come. as you know government and bureaucracy things
3. Not that we i handled the traige during the booking system so instead of incremental numbers we had them in groups of 5 so say one guy comes and get the number 001 and the next one would get 006 now what happens is in the slot 001-005 it corresponds to the priority of the patient like 001 for the emergency guy and 004 for the medocAppointment and 005 for the general person. Now in case if there are numbers empty in the list then it won't simple reflect in the doctor's schedule say on the doctor's side he sees
today's appointments
001 - Mr. X
002 - Miss y
004 - Mr. John
006 - Mr David
so  they'd call up as such.
before i go over that i'll give you a detailed description of my work at appable
they had 3 apps and 2 backends i was hired as frontend  dev ended up doing the whole full stack even to the systems design cause they though thatthey'd just use API's like firebase but it came out to be costly so i had to make a custom Backend so i'll walk you though those 2 projects that i worked in appable over the year and then we'll go back to the KMS
proj1 : this i was a pair of mobile apps with customer-client apps the app's main goal was to book grounds and stadium for matches and tournaments by the local people like say a colony looking for their annual games or a comapny looking for a company outing thing. so main thing was there were 2 kinds of events open and closed. in closed one the creator invites people by phone number if they are on the app they'll get a notification in app using the Push notification and then they open it in app to accept or reject. or you can send SMS with a format to the phone number if the user is not registered on our app. yes we used phone  number as a unique identifier. then the open one creates an event with a date you can create events with any date the constraint was startDate < EndDate then the deadline to join was 2 days before the event the creator can restrict the open to open to all so you can join with just click of a button and pay the fee. or you can restrict and it sends a request to the creator of the event to accept you as a participant. then it had a chat for that event which is only active till the event is active. and then there are tournaments but they are mostly closed by nature. when creating events you can look up grounds on our app using the Map layout that we are using we used google map for our maps and then laid out our grounds using Map custom pin feature. and also added a direction feature where it'd launch the direction URL of the selected pin so you can navigate using your applemaps or googleMaps app. then on the client side (wiz. the ground owner) he can add his grounds to our app and it's have a calendar interface to show which events are when on which ground. (The calendar interface was on the client side as well to know his schedule for events he signed up for) and then he can approve requests for people who wanted to have events on his grounds on the listing he gives prices like per hr or per day. you can also make teams with your friends and when creating a sport event you can select the teams you wanna be with and it'll invite all the people on the team. but each team had a role called team manager by default it's the guy who creates the team but he can add others as the manager and only the managers can add teams to the events. when you create a team and add players to it again the same thing they'll get request if they are on the app or an sms invite if they aren't. the SMS would have 2 links one to the playstore if they don't have the app and if the app is there then just shows them their notification page which on load fetches all the new requests. we also asked for permission to contacts so you can't just search for a 10 digit phone number and send an invite to that. you can use a phone number to search but the invite button would only show up if the person is on our app or in your contacts. The backend was node.js REST apis and DB was mongo DB i was the sole Dev so i designed the frontend, build/code it and designed and code the backend and the DB schema as well techs tack : flutter (mobile apps) node.js (backend) and MongoDB
proj2: This was an HRMS app for a local business it had 3 components (1 backend, 1 mobile app, 1 web based admin app) the mobile app has attendance add, see, leaves of all types and salary status. in the DB each person had a designation and list of people under them. so when someone logs in with the employeeid and password and DB fetches their profile records it also fetches their designation and ids of people under them but say there's a 2nd tier manager with 2 layers of people under him then he'll get the id's of all the people that are under him directly and the people under those. the interface for the admin/manager was different from the regular one on regular one you can only request for leaves, sick leave, outstation, client visit and see the status of your request the admin had a section on the mobile app to approve or deny these requests. and here again i need to make priority system because if a 2nd tier manager refused your request then the acceptance of a tier 3 manager won't override that. all the employees also had the ability to upload their docs like PAN, adhaar, etc through our app if the demands it. the attendance was the main feature where you had to take a selfie and it records dateTime, image, empid and geolocation as well. since the attendance is geofenced you need to be in the office else you won't be able to submit your attendance. and if you do it more than 3 times consecutively then it'd notify your senior about it. the only time you are allowed outside was when there was a client visit approved on your calendar for that date. and you have to log both in and out time for your attendance or the system would flag it. and there wasn't a saperate button for in time and out time the logic was in your record there was your shift time in and out in 24 hr format and we just calculate if you are closer to which time and then report wether you are late to the shift or early to the shift. so this way it records overtime as well and penalizes freeloaders. then there was a cron job that ran on 23:55 everyday and it fills in the default value (midnight) in the slots that were empty to do 2 things marks absent on the ones that weren't present and also mark out the ones that had a day shift but didn't clocked properly like left office without clocking out. this cron then again ran on 11:55 for the night shift people of the last night. then the admin portal had the same thing but with added feature to add employees, update their info like phone number, address, department, salary, or add employees in bulk using the sample xlsx sheet. approve leaves and outing singularly or select them and approve/deny in bulk. dashboard to see the attendance stats of the day/week/month or any specific month, see attendance records with images fitering by date/department/name/empId/date-range. it can also generate salary slips as a pdf so you can generate it for all the employees or by department or by date range or for just one employee and any combination of these. the result would be a single pdf with all the salary slips that fit your filter criteria and you can then print it or send them.
tech stack : mobile app - flutter
backend node-js
web-admin : EJS
DB : postgresSQL
images are stored in drive using the format $images/data/attendance/date/department/empid.jpg
and the medoc apps's tech stack was
mongodb for Database with FlutterSharedPrefences for local storage
Flutter for mobile and web apps (there were 2 repos 1 mobile app , 1 for a webapp)
backend - node.TS
and the Techasoft people moved their DB to postgres from SQLITE and the frontned and backend uses REST API to communicate cause there weren't compentent devs to understand IPC protocols since both of them run on the same machine the fronend just calls localhost:8080 (not the actual port)
1. key rotation so i implemented it as follows : every day the go app runs a cron job and reads the ./keystore dir and checks for files created before 30 from time.now() and then it re-writes the file name to {keyId}_deact.key so that when the backend app calls the update key route it generates a new key and stores it as {keyId}.key (this is not the new key id the key id is only created at the createKey route only the DEK and IV are updated). then it sends the new and old keys encrypted with the backend's master key back to the backend app and marks the _deact key with _deact_del the reason i'm not deleting yet is cause if say their app faults or the network faults and i had deleted it already then the data that was there would be rendred useless and un-accessible as the that encrypted it was now gone so this _del version stays till 24 hrs and on the next cron job it gets deleted. now when the bakcend migrates it their flow looks like on key rotation job db.getRecord() -> updateKey ->  decrypt payload using the master key -> decrypt using the old key -> encrypt the record using the new key and db.writeUpdate() now the only lives in the backend's memory not even the cache as the KMS sends the key on getKey in under 2ms
2. yes there is an app master key that i personally rotate every 3 months that encrypts the DEK store locally
3. yes the master key is derived using a passphrase from pbkdf2
4. i am using a mutex protected map but since most of the things don't live in memory and are read on demand from the drive the concurrency just comes when i use Echo for http requests
Added note the next project after this is Accounting software one so that was just a backend with no frontend so you can keep it in the tradtional dev version but i have an AI freindly thing called LLVM-compiler where i tried making a compiler for my toy-lang in Ocaml-rust and llvm using Gemini Antigravity. and there's also a simple C++ sfml games collection i made in learning so if you think that's fitting then we can go with that also maintain the context of the projects cause i'm gonna need you to give detailed descriptions for them so i can go more detailed about them in my CV and my portfolio site plus i can then use those desc to get readme files later on through some another agent.
now the Personal Bahi Khata app
tech Stack  : flutter
description working : you add your expense manually using a form interface and then it adds it to a list of Expense Objects this then gets converted to a json string and compressed using Zstd compression level 13 then ecnrypted using a key-iVgenerated on the spot and   final int TAG_LENGTH = 16;
final int SALT_LENGTH = 16;
final int KEY_ITERATIONS_COUNT = 10000; AES-GCM enc then the data is stored in a local file called fins.pbke this is a proprietory file format
the pbke file has the following layout
signature = "%PBKE%"   (6 bytes)
time = 4 bytes (Unix timestamp, big-endian)
encryption = AES-GCM
legacy version :
signature = "%PBKE%"
version   = (NOT present)
time      = 4 bytes
[ HEADER - 23 bytes ]
signature (6)
time (4)
padding (13 zeros)
[ ENCRYPTED PAYLOAD - variable ]
AES-GCM(zstd(compressed JSON))
[ FOOTER - 44 bytes ]
IV  (12 bytes)
KEY (32 bytes)
latest version  :
signature = "%PBKE%"
version   = "01_10"
time      = 4 bytes
[ HEADER - 16 bytes ]
signature (6)
version   (6)
time      (4)
[ ENCRYPTED PAYLOAD - variable ]
AES-GCM(gzip(compressed JSON))
[ FOOTER - 44 bytes ]
IV  (12 bytes)
KEY (32 bytes)
for the SMS it reads all the sms untill the last date of file write and looks or keywords such as ['credited',
'debited',
'transfer',
'withdrawal',
'deposit',] then looks for a number and adds it to the amount. now you can also edit this expense records so if something is messed up you can correct it and since on everysave it stores the last write you can avoid duplicates as the id of expense is given by me.
it aslo has a search feature where you can filter the expenses using the month-year and tags. also it shows the monthly balance since you can label each entry as a credit or debit it shows a monthly balance in the UI as well so you can get an idea of your accounts without crunching numbers
it also has a share feature where you can select a date range and share the expenses as a pbke file or a csv. since pbke can only be read by my app i gave csv/json as an open alternative for cross compatibilty.
the language is strongly type functional language  with minimal keyword but excellent std lib support so as the base language remains easy and allows you to build on top. it has Types and Enums are Taged unions like Rust or haskell you can define typeClasses like haskell and lists are handled like haskell. it has rust's borrowchecker and vairable/functions are scoped like Std.Math.Trig so you can import Std.Math and call Trig.sin or the whole thing then just call sin() the name resultion requires an alias if there are naming conflicts like 2 modules imported in a file that has the sin name cause internally the compiler stores them as Std.Math.Trig.sin and Start.start. the root is a module called start and root function is start. it reutrns nothing. it's a pure function. there are functions that must return a value or procedures that just do stuff returns Unity (). a procedure can't modify outisde the scope unless the var is defined as mut. a var can never be modified, types and module names are `Std` this case, keywords are all lowercase and var and functions/proc must start with a lowercase a-z , NULL is a different type it doesn't throw garbage value like C.
so i just gave the gemini the grammar rules on how the source code would look and i just told her to implement it with rust+haskell like model and told her exactly what i wanted from each one and how dead-code removal should be done via tree shaking before compiling the final binary resulting in a bin with minimal signature. i wanted to add support for BCD like numbers to be precise with calculations in order to avoid floating point arithmatic but that would be in the Math.Integers module scopes are defined by {} and the return keyword is `=>` so in a function block if you write => a+2 then it'd return it and exit or you can define function as lambda exp like func myFunc(x:int8,y:int8)->int32 = x^y; semicolon in necessary
okay but on tradtional dev one we'd only have 2 projects as the LVm compiler thing is only the AI dev roles so from the list i gave you in preivous prompts ask me about one more project that we are to add in there also i have a bunch of Linux diy's like my dotfiles to replicate my arch setup and grub theme, ssdm, theme, noctalia shell plugin, some nvim plugin, plymouth themes and a Go based anonymous forum site like 4 chan (it's live hosted) with HTML templating and server rendering
1. Yes using the html/template. There are no file uploads yet.
2. There is no persistent data you can use a passcode like #aba# and this will be hashed into a 16char string that will be your unique identifier. There is an optional name field and say you choose to make post by the name josh and there's someone else who can use the same name as you. Your name is only reserved till your session is active. Once you close the browser window your name is open to all but since the passcode is unique so when you type your name as josh #aba# and say it gets hashed into josh #123hGf... This string will be unique. The final hash is then string manipulated to fit under this range [A-Z][a-z][0-9]. And it also supports md rendering so you can use common mark to highlight some text or use other formatting mechanism. This way when you put http/https links in your text and a user clicks it . It takes them to a warning page that this link will redirect you to <hostname> and we don't hold any responsibility of your actions over there
3. The nvim plugin is just a linter for my custom text based data format for a personal record. My other linux works like noctalia shell plugins they optimize the flow by embedding the input type change (i.e changing my keyboard from US to itrans hindi or JP or Sanskrit) for multilingual works. And instead of opening the fcitx app I can just do it from my status bar. And the other 2 are themes written in qt-qml for sddm and grub one for each.
Draft for the AI dev version first
Yes you need to update the work timeline since we removed appable you can add my work as product lead in medoc during the time between the software intern and project management. In that time you can mention about the work I did on their eua app the one with prescription and appointments and all that and next we'll move to the projects section
I think you should also add the personal bahi khata app or the Go forum site as well if there's space for it and also update the professional summary. Cause even in ai centric roles I'm more likely to apply for a backend dev especially in Go so that and in the next prompt give me these things and after that we'll get the latex
sure give me the latex code for version 1 and you can either give it as a main.tex file that i can download or a code block that i can copy and paste on overleaf
edits :
- remove the [cite:1] blocks
- Add hbar or hrule under each section Header
- Make the project title more visible in the mix
- give me space to link either the github or Deployed version of things and with github use the github fav icon and deployed is only personal bahi khata and that is on play Store so  use that favicon. also other can code can you explain that since i told you that this Resume is AI+go+systems engineering so why did we used Personal Bahi khata and not the Forum site made in Go
reduce the margins by half and the hrule is overlapping with the Section name is should be under the name
remove [cite:1] and technical skills should all be aligned at the same indet from the left and also on the same indent after the colon use a bordless table for layout
it is taking the education section on to the second page we want the whole thing to be one page in A4 layout
Great work and now give me the latex for version 2 as well
I'm gonna tell you about another project call GOD (or grounded object notation) i think this would be a good fit for the backend role i was pissed off with json and it's redindancy so i designed this  for data over text here are it's full grammar spec and tell me which version it'll fit in
# GOD (Grounded Object Data) Formal Grammar Specification
**Version:** 1.0.0
**Date:** December 2025
**Status:** Final Draft
## 1. Introduction
GOD (Grounded Object Data) is a lightweight, human-readable data serialization format designed as a more compact and safer alternative to JSON. It provides native support for tabular data and enforces "grounded" semantics where every data point corresponds to a concrete value (zero values) rather than undefined or null states.
### 1.1 Design Goals
- **Grounding**: All data points are grounded in concrete types. There is no `null` value; omitted fields return the type's zero value.
- **Compactness**: Significantly reduce data size compared to JSON, especially for repetitive structured data.
- **Readability**: Maintain a syntax that is easy for humans to read and write.
- **Tabular Power**: First-class support for columnar/tabular data.
- **Space Efficiency**: Optimized for storage and transmission.
### 1.2 Key Differences from JSON
| Feature | GOD | JSON |
|---------|-----|------|
| Null values | ❌ Omitted = Zero values | ✅ Explicit null |
| Tabular data | ✅ Native `(header:rows)` | ❌ Array of objects |
| Keys | ✅ Optional for single values | ✅ Always required |
| Root requirement | Must be object `{}` | Any type |
| Safety | ✅ Safeguard against null | ⚠️ Allows null values |
## 2. Lexical Structure
### 2.1 Character Set
GOD uses UTF-8 encoding.
### 2.2 Whitespace
Whitespace characters (space, tab, newline, carriage return) are insignificant except within string literals.
### 2.3 Tokens
```
token ::= '{' | '}' | '[' | ']' | '(' | ')' | '=' | ';' | ',' | ':' | string | number | boolean | identifier
```
## 3. Grammar Rules
### 3.1 Root Structure
**Rule 1**: The root element MUST be an object enclosed in braces `{}`.
**Rule 2**: If the object root contains more than one value, all values MUST have a key.
**Invalid:**
```
{"John"}         ✅ Valid (single value)
{"John", 25}     ❌ Invalid (multiple naked values)
{name="John", 25} ❌ Invalid (mixed keyed and naked)
```
**Valid:**
```
{name="John"; age=25} ✅ Valid (all keyed)
```
### 3.2 Objects
An object contains content enclosed in braces.
```ebnf
object ::= '{' content '}'
content ::= raw-value | key-value-pairs | empty
raw-value ::= value
key-value-pairs ::= key-value-pair (term key-value-pair)* term?
term ::= ';' | whitespace+
```
### 3.3 Values
```ebnf
value ::= string | number | boolean | object | array | table | empty
```
### 3.4 Key-Value Assignment
Assignment uses the `=` operator.
```ebnf
key-value-pair ::= identifier '=' value
identifier ::= [a-zA-Z_][a-zA-Z0-9_]*
```
### 3.5 Strings and Characters
- **Strings**: Must be in double quotes `"`.
- **Characters**: Can be in single quotes `'` or double quotes `"`.
- **Multiline**: Supported using triple quotes `"""`.
```ebnf
string ::= '"' char* '"' | '"""' multiline-char* '"""'
```
### 3.6 Arrays (Lists)
Arrays contain comma-separated values in brackets `[]`. Mixed types are allowed.
```ebnf
array ::= '[' (value (',' value)*)? ']'
```
### 3.7 Tables (Tabular Structured Data)
**Rule 13**: Tables provide an efficient way to store lists of similar objects.
```ebnf
table ::= '(' header ':' rows ')'
header ::= identifier (',' identifier)*
rows ::= row (';' row)* ';'?
row ::= cell (',' cell)*
cell ::= value
```
**Example:**
```
users = (id,name,age:01,"alice",20;02,"Bob",23;);
```
## 4. Grounding and Zero Values
**Rule 18**: The core philosophy of GOD is that every field is grounded. When data is missing or empty, it is automatically assigned the type's zero value.
| Type | Zero Value | Marshalling |
|------|------------|-------------|
| **Integer** | `0` | `0` |
| **Float** | `0.0` | `0.0` |
| **String** | `""` | `""` |
| **Boolean** | `false` | `false` |
| **Unknown** | `""`| `""`|
If a field is empty (e.g., `errorCode = ;`), it is marshalled with the `\0` character.
## 5. Usage Example
```
{
status = 200;
request = "POST";
error = "";
errorCode = ;
data = {
roles = ["admin", "super"];
users = (id,name,age:01,"alice",20;02,"Bob",23;);
}
}
```
## 6. License
GOD is free for personal, creative, and educational use. Commercial use requires prior permission from the developer. See the [LICENSE](LICENSE) file for full terms.
okay so just give me the latex code for this Project and tell which one to replace in which version
\documentclass[a4paper,10pt]{article}
\usepackage[left=0.25in,right=0.25in,top=0.25in,bottom=0.25in]{geometry}
\usepackage{enumitem}
\usepackage{xcolor}
\usepackage[hidelinks]{hyperref}
\usepackage{titlesec}
\usepackage{fontawesome5} % For GitHub and Play Store icons
\usepackage{tabularx}     % For aligned layout of Technical Skills
\definecolor{myblue}{HTML}{23407C}
\pagestyle{empty}
% Absolute tightest list spacing to guarantee single-page constraint
\setlist{noitemsep, topsep=0pt, parsep=0pt, partopsep=0pt, leftmargin=1.1em}
% Compressed section spacing
\titleformat{\section}{\large\bfseries\color{myblue}}{}{0pt}{}[\vspace{1pt}\hrule]
\titlespacing{\section}{0pt}{4pt}{2pt}
\begin{document}
\begin{center}
{\LARGE \textbf{VINAYAK GUPTA}} \\
\vspace{0.5pt}
\small
Chhapiheda, Rajgarh (MP) \; \textbar \; +91-70490-49698 \; \textbar \; \href{mailto:vinayakg236@gmail.com}{vinayakg236@gmail.com} \\
\vspace{1pt}
\footnotesize
\href{https://github.com/vinayakgupta29}{\faGithub\ github.com/vinayakgupta29} \; \textbar \; \href{https://linkedin.com/in/vinayak-gupta-70a808202}{\faLinkedin\ linkedin.com/in/vinayak-gupta-70a808202} \; \textbar \; \href{https://vinayakgupta29.github.io/portfolio}{\faGlobe\ Portfolio}
\end{center}
\vspace{-6pt}
\section{Professional Summary}
\small
Software Engineer with ~3 years of experience specializing in robust backend architectures, distributed systems, and cross-platform web/mobile systems using Go, Node.js, and PostgreSQL. Proven track record designing low-latency cryptographic microservices, optimizing concurrent data layers, writing custom multi-platform tooling, and implementing scalable workflows for infrastructure and healthcare platforms supporting over 40k users. Expert in systems design, API engineering, and hardware-software hardware orchestration.
\section{Technical Skills}
\small
\renewcommand{\arraystretch}{1.0} % Compressed row spacing
\noindent
\begin{tabularx}{\textwidth}{@{} p{3.2cm} @{\hspace{0.1cm} : \hspace{0.2cm}} X @{}}
\textbf{Languages} & Go, TypeScript, JavaScript, Python, SQL, Java, C++, Rust, OCaml \\
\textbf{Backend \& Systems} & Node.js (Express/TS), Django, Echo (Go), REST APIs, Systems Design, Microservices, Cron/Automation Pipelines \\
\textbf{Frontend \& Mobile} & Flutter, Tauri (.deb), React, EJS, HTML5/CSS3, Multilingual Status-Bar Plugins \\
\textbf{Databases \& Cloud} & PostgreSQL (High-Concurrency Optimization), MongoDB, SQLite, AWS (EC2/S3), Docker, Git, Linux (Arch/Nvim customization) \\
\end{tabularx}
\section{Experience}
\small
\textbf{Techasoft Pvt. Ltd.} \hfill Bangalore, India \\
\textit{Software Development Intern (Systems \& Integration)} \hfill Mar 2026 -- Present
\begin{itemize}
\item Architected the full-stack system layout for industrial plant automation, configuring a Django backend and compiled Tauri (.deb) frontend to execute on native Linux client environments.
\item Engineered high-performance hardware-software control loops using Python (Modbus TCP), orchestrating low-latency 24V PLC signaling within an 8ms window to drive conveyor sorting systems.
\item Designed an offline calibration layer inside Django, calculating dynamic pixel-to-millimeter Region of Interest (ROI) coordinate configurations to ingest real-time frame rates up to 30 FPS.
\item Executed database migrations from SQLite to PostgreSQL, resolving severe pipeline bottlenecks and stabilizing database write concurrency for production-floor metric logging.
\end{itemize}
\vspace{1.5pt}
\textbf{Medoc Health IT} \hfill Remote \\
\textit{Engineering Product Lead \& Project Management Intern} \hfill Jul 2024 -- Jul 2025
\begin{itemize}
\item Built a low-latency local Key Management System (KMS) in Go via the Echo framework, implementing PBKDF2 master key derivations to yield sub-2ms cryptographic key retrieval times.
\item Navigated legacy government specifications to integrate ABHA v4 health data APIs, mapping complex tokenized JSON schemas for an encrypted data environment serving 40,000+ patients.
\item Architected the core scheduling architecture of the MedocEUA application, implementing a sparse-allocation bitwise slot priority algorithm ($2^n - 1$) to manage high-volume emergency triage queuing.
\item Authored cross-platform mobile modules in Flutter, integrating background hardware data synchronization protocols via the Android Health Connect API and secure decentralized user consent managers.
\end{itemize}
\vspace{1.5pt}
\textbf{Appable Technologies} \hfill Remote \\
\textit{Freelance Full-Stack Software Developer} \hfill Jul 2023 -- Jun 2024
\begin{itemize}
\item Re-architected multiple client applications away from high-cost Firebase structures into custom Node.js and PostgreSQL backends, lowering infrastructure spend by hosting custom web dashboards.
\item Designed a recursive organizational hierarchy engine in PostgreSQL to compute nested supervisor permissions and tiered multi-level manager approval lines for an enterprise HRMS.
\item Built an offline-first geofenced attendance logging system using camera biometric validation and real-time shift-delta analytics, utilizing automated cron pipelines to process bulk system actions.
\item Developed an isolated sports booking platform supporting custom Google Maps markers, dynamic hourly pricing grids, and asynchronous SMS invitation fallbacks for unregistered users.
\end{itemize}
\vspace{1.5pt}
\textbf{Medoc Health IT} \hfill Remote \\
\textit{Software Development Intern} \hfill Aug 2022 -- Jul 2023
\begin{itemize}
\item Maintained core healthcare application features using Flutter, Node.js, and SQL, improving deployment efficiency by provisioning containerized environments with custom Docker compose files.
\end{itemize}
\section{Projects}
\small
\textbf{\large Zundrath Key Management System} \hfill \href{https://github.com/vinayakgupta29/zundrath}{\faGithub\ Code} \\
\textit{Go, Cryptography, Echo Framework, PBKDF2}
\begin{itemize}
\item Developed a local cryptographic microservice serving concurrent clients with sub-2ms retrieval latency via mutex-protected on-demand disk indexing.
\item Implemented a fault-tolerant, two-phase key rotation pipeline providing a 24-hour safe-migration window to eliminate decryption blackouts during live application schema updates.
\end{itemize}
\vspace{1.5pt}
\textbf{\large Anonymous Live Forum} \hfill \href{https://github.com/vinayakgupta29/link-here}{\faGithub\ Code} \\
\textit{Go, html/template, Session Architecture, Markdown Parser}
\begin{itemize}
\item Built a stateless, live-hosted textboard using Go's native \textit{html/template} package for server-side rendering, avoiding persistent state overhead.
\item Developed a secure tripcode authentication system that hashes user passphrases into unique 16-character identifiers matching strict alphanumeric ranges ($[A-Z][a-z][0-9]$).
\item Integrated an intermediate client protection proxy layer that parses Markdown hyperlinks and forces mandatory target-destination warning redirects to insulate system safety.
\end{itemize}
\vspace{1.5pt}
\textbf{\large Grounded Object Data (GOD) Format} \hfill \href{https://github.com/vinayakgupta29/god-notation}{\faGithub\ Code} \\
\textit{Go, EBNF Grammar, Lexical Scanner, Reflection API}
\begin{itemize}
\item Designed and engineered a lightweight, schema-less data serialization format utilizing a strict EBNF grammar specification to eliminate JSON payload redundancy and reduce data transmission footprints.
\item Implemented a hand-written lexical scanner and recursive-descent parser in Go, introducing native, first-class tabular structures \texttt{(header:rows)} that strip repetitive object keys from multi-row payloads.
\item Enforced strict "grounded" type-safety semantics within the marshalling engine, structurally preventing null-pointer runtime panics by automatically initializing missing fields to zero-values or explicit \texttt{\textbackslash 0} null-terminators.
\end{itemize}
\section{Education}
\small
\textbf{B.Tech in Computer Science and Engineering} \hfill 2025 \\
LNCT University, Bhopal
\end{document}
this V2 code is now in 2 pages so format it down to 1 page in A4 and page margins on all sides should be 0.25in
still on 2 pages the education section as a whole is in the second page
reduce the techasoft work to 2 points as a backend dev
still the education section is in the second page
both of them are bad now there's like 1/3 of the page is empty
thanks it is better now. Now i want to work on my portfolio site and CV so can you give me the Professional Summary (make one that compiles the ideas from both resumes) + Work Experience(all of it) + Projects all of them in latex sections and go as much detailed as you can and showcase the variety of skillset that i have in all aspects computing, programming, languages, linguistics, mathematics and optimizations
now also give me a Skills section listing technical and non technicals in the same section and also i have a custom command called \sectionlabel so use that instead of section
so i am also leaning japanese and in dec i'll get a N3 certificate and i can fluently speak like 5 other languages and this can become an asset in both versions of the resume so where and how can i mention it in both of them with my certification level like Japanese(N3), English(IELTS-8.3)... etc
Now this whole conversation we have I'm gonna give it to another chat to gain context for something else so whatever's I have described so far can you find some way that I can export this conversation to them or can I just share the public link directly and the model would be able to read it given they can fetch the data from the link?
No bro I want the whole context the whole details I gave to you about my work and projects every word as is
```
